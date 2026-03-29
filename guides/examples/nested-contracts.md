---
title: Nested Contracts
description: Use Contract-typed fields to model structured sub-sections of a page.
---

Target: [Mountainhome Herald](https://qscrape.dev/l1/news) (QScrape L1)

When a page has logically distinct sections — an article's body and its author byline, a product listing and its seller info — you can model each section as its own contract and nest one inside the other. Yosoi flattens nested fields to `{parent}_{child}` keys for discovery, so the LLM sees a single flat list of fields while your code keeps a clean, grouped structure.

## Defining a Nested Contract

A nested contract is just a `Contract` subclass used as a field type on another contract. The child contract can optionally pin its own `root` to scope its selectors within a specific container on the page.

```python
# article_with_author.py
import asyncio
import yosoi as ys

class AuthorInfo(ys.Contract):
    """Author byline section of an article."""
    root = ys.css('div.author-byline')  # scope selectors to the byline container

    name: str = ys.Author(description='Author display name')
    role: str | None = ys.BodyText(description='Author role or title (e.g. "Senior Reporter")')

class Article(ys.Contract):
    """News article with structured author info."""
    title: str = ys.Title(description='Article headline')
    date: str = ys.Datetime(description='Publication date')
    summary: str = ys.BodyText(description='Article summary or lede')
    author: AuthorInfo = AuthorInfo  # nested contract
```

When Yosoi runs discovery, it flattens the fields to:

| Discovery key | Source |
|---|---|
| `title` | `Article.title` |
| `date` | `Article.date` |
| `summary` | `Article.summary` |
| `author_name` | `AuthorInfo.name` |
| `author_role` | `AuthorInfo.role` |

The LLM discovers selectors for all five fields in one pass. During extraction, Yosoi re-nests the flat results back into the `AuthorInfo` structure.

## Running It

```python
async def main():
    pipeline = ys.Pipeline(ys.auto_config(), contract=Article)

    async for item in pipeline.scrape('https://qscrape.dev/l1/news'):
        print(item.get('title'))
        author = item.get('author', {})
        print(f"  by {author.get('name')} ({author.get('role')})")

asyncio.run(main())
```

```bash
uv run python article_with_author.py
```

Or from the CLI with a custom contract:

```bash
uv run yosoi --url https://qscrape.dev/l1/news --contract article_with_author.py:Article --output json
```

## With vs. Without a Pinned Root

The child contract's `root` controls where its selectors are scoped:

| | Pinned root | No root |
|---|---|---|
| **Behaviour** | Child selectors are resolved relative to the `root` element | Child selectors are resolved against the full page (or the parent's root) |
| **When to use** | The child data lives in a visually distinct container (byline, sidebar, card footer) | The child fields are interleaved with parent fields in the same container |
| **Discovery hint** | Yosoi tells the LLM: *"Scope these fields within `div.author-byline`"* | Yosoi tells the LLM: *"These fields are co-located with the parent fields"* |

To let the AI discover the child's root instead of pinning it:

```python
class AuthorInfo(ys.Contract):
    root = ys.discover()  # AI picks the container
    name: str = ys.Author()
    role: str | None = ys.BodyText()
```

## When to Use Nested Contracts

Use nested contracts when:

- **Grouping matters for your downstream code.** Instead of accessing `item['author_name']` and `item['author_role']` as flat keys, you get `item['author']['name']` and `item['author']['role']`.
- **The child section has its own root element.** Pinning a root on the child contract scopes discovery and improves selector accuracy for data that lives in a distinct container.
- **You want to reuse the child contract.** The same `AuthorInfo` contract can be nested into `Article`, `BlogPost`, `PodcastEpisode`, etc.

For flat pages where all fields live at the same level, a single contract with no nesting is simpler and works just as well.

## FAQs

<details>
<summary>Can I nest more than one level deep?</summary>

Yes. A nested contract can itself contain Contract-typed fields. Keys are flattened recursively: `parent_child_grandchild`. Keep nesting shallow (two levels max) to avoid discovery prompts that are hard for the LLM to follow.

</details>

<details>
<summary>What happens if the nested root selector doesn't match?</summary>

If a pinned root doesn't match any element on the page, all child fields return `None`. Run with `--debug` and inspect the HTML to verify the container exists. If the site layout changed, update the pinned root or switch to `ys.discover()`.

</details>

<details>
<summary>Can I mix nested contracts with list fields?</summary>

Yes. A field typed as `list[ChildContract]` works the same as `list[str]` — Yosoi extracts multiple instances of the child structure. Each instance is flattened for discovery and re-nested during extraction.

</details>
