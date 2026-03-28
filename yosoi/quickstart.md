---
title: Quick Start
description: Discover and use CSS selectors in minutes.
---

## Discover selectors for a site

```bash
uv run yosoi --url https://news.ycombinator.com
```

Yosoi fetches the page, asks the LLM to identify selectors, validates them, and saves the result to `.yosoi/`.

## Scrape articles using discovered selectors

```python
from yosoi import Yosoi

yosoi = Yosoi()
articles = yosoi.scrape("https://news.ycombinator.com")

for article in articles:
    print(article.headline, article.url)
```

Discovery only happens once per domain. Subsequent calls read from the local cache — no LLM calls, no cost.

## CLI reference

| Flag | Description |
|------|-------------|
| `--url` | Target URL to discover selectors for |
| `--provider` | LLM provider to use (e.g. `groq`, `openai`) |
| `--debug` | Save extracted HTML to `.yosoi/debug_html/` |
