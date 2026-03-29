---
title: Debugging
description: Diagnose and fix selector discovery failures, extraction errors, and common issues.
---

When something goes wrong, Yosoi gives you a few tools to figure out what happened and where. This guide covers the `--debug` flag, common failure modes, and how to recover.

## The `--debug` Flag

Pass `--debug` (or `-d`) to the CLI, or set `debug=True` on the `Pipeline` constructor, to save a snapshot of the HTML that was sent to the LLM:

```bash
uv run yosoi --url https://example.com --contract Product --debug
```

```python
pipeline = ys.Pipeline(ys.auto_config(), contract=Product, debug=True)
```

Snapshots are saved to `.yosoi/debug_html/` as plain HTML files, named by domain and timestamp. Open them in a browser to see exactly what the LLM was working with.

## Common Failure Modes

### 1. API Key Invalid or Missing

**Symptoms:** An authentication error from the LLM provider immediately after discovery starts.

**Fix:** Check your `.env` file. The key name must match the provider format: `GROQ_KEY`, `GEMINI_KEY`, `OPENAI_KEY`, etc. Run with a simple test URL to confirm the key works before debugging anything else.

### 2. Target URL Is Inaccessible

**Symptoms:** Empty or near-empty debug HTML. The LLM returns selectors that don't match anything.

**Fix:** Open the URL in a browser. If it requires JavaScript to render, Yosoi's static fetcher won't see the content. You need to pass pre-rendered HTML via a browser automation tool (Playwright<sup>[△](#ref-1)</sup>, Selenium<sup>[○](#ref-2)</sup>) or wait for the upcoming DOM-enabled scraping feature (see [Roadmap](/roadmap/)).

### 3. Wrong Root Selector

**Symptoms:** Multi-item extraction yields one giant item (root too broad) or many items with mostly `None` fields (root too narrow).

**Fix:** Pin the root on your contract after inspecting the page source:

```python
class Product(ys.Contract):
    root = ys.css('article.product')  # pin the correct container
    name: str = ys.Title()
    price: float = ys.Price()
```

See [E-Commerce Catalogue: Automatic vs. Pinned Root](/guides/examples/e-commerce/#automatic-vs-pinned-root) for a detailed walkthrough.

### 4. Stale Selector Cache

**Symptoms:** Extraction used to work but now returns `None` for some or all fields. The target site has been redesigned.

**Fix:** Force re-discovery to clear the cached selectors for that domain:

```bash
uv run yosoi --url https://example.com --contract Product --force
```

```python
pipeline = ys.Pipeline(ys.auto_config(), contract=Product, force=True)
```

You can also manually delete the cache file from `.yosoi/selectors/` and run again.

### 5. Context Window Overflow

**Symptoms:** The LLM returns truncated, garbled, or missing selectors. Large pages with deeply nested HTML are most susceptible.

**Fix:** There is no built-in mitigation yet (see [Smart Batching](/roadmap/) on the roadmap). Current workarounds:

- Use a model with a larger context window (e.g. Gemini<sup>[◑](#ref-3)</sup> models with 1M+ tokens)
- Trim the HTML yourself before passing it in
- Target a more specific page (e.g. a category page instead of the homepage)

### 6. Coercion / Validation Errors

**Symptoms:** Pydantic<sup>[◇](#ref-4)</sup> `ValidationError` with field-level details. The selector matched, but the extracted text couldn't be coerced to the field's type.

**Fix:** Run with `--debug` to see the raw extracted values. Common causes:

- A `float` field receives text like `"$12.99"` but the coercion type doesn't strip currency. Use `ys.Price()` instead of a bare `float` field.
- A field expecting a single value receives a list (or vice versa). Check whether the field should be `list[str]` or `str`.
- A custom type's `coerce` function doesn't handle edge cases. Add a descriptive `ValueError` to surface the issue.

## Inspecting the Selector Cache

Cached selectors live in `.yosoi/selectors/` as JSON files, one per domain. You can read them directly to see what the LLM discovered:

```bash
cat .yosoi/selectors/qscrape.dev.json | python -m json.tool
```

Each entry maps a field name to a selector string. If a selector looks wrong, you have two options:

1. **Edit the cache file** directly and re-run extraction (no LLM call needed)
2. **Pin the selector** on the contract with `yosoi_selector` and force re-discovery

```python
from pydantic import Field

class Product(ys.Contract):
    name: str = Field(
        description='Product name',
        json_schema_extra={'yosoi_selector': {'primary': 'h2.product-title'}},
    )
```

## Checklist

When something breaks, work through this in order:

1. Run with `--debug` and inspect `.yosoi/debug_html/`
2. Open the target URL in a browser — is the content visible without JavaScript?
3. Check `.yosoi/selectors/` — do the cached selectors look reasonable?
4. Try `--force` to re-discover from scratch
5. Pin the `root` if multi-item extraction is off
6. Switch to a larger-context model if the page is very large

## References

<a id="ref-1"></a>△ **Playwright**. Microsoft. *Browser automation library for end-to-end testing and web scraping.* https://playwright.dev/python/

<a id="ref-2"></a>○ **Selenium**. OpenQA. *Browser automation framework for web testing.* https://www.selenium.dev/

<a id="ref-3"></a>◑ **Gemini**. Google. *Large language model family with extended context windows.* https://ai.google.dev/

<a id="ref-4"></a>◇ **Pydantic**. Pydantic Services Inc. *Data validation library for Python.* https://docs.pydantic.dev/
