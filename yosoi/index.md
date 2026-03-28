---
title: Overview
description: AI-powered CSS selector discovery for web scraping.
---

Give Yosoi a URL and it uses an LLM to automatically discover the best CSS selectors for extracting headlines, authors, dates, body text, and related content from any site.

- **Fast** — 3 seconds to discover selectors per domain
- **Cheap** — ~$0.001 per domain (one-time cost)
- **Reusable** — selectors are cached locally; scrape thousands of articles for free after discovery

## How it works

1. You provide a URL
2. Yosoi fetches the page HTML and sends it to an LLM
3. The LLM identifies stable CSS selectors for each content field
4. Selectors are validated and stored in `.yosoi/`
5. Future scrapes use the cached selectors directly — no LLM call needed
