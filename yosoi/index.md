---
title: Introduction
description: AI-powered CSS selector discovery for web scraping.
---

**Yosoi** stands for **You Only Scrape Once (iteratively)**. The name captures the core idea: pay for LLM-based selector discovery once per domain, then scrape that domain forever using the cached selectors with no further AI cost.

The "iteratively" part matters. When a site redesigns and cached selectors go stale, Yosoi detects the breakage, re-discovers only the fields that changed, and merges the fresh selectors back into the cache. You pay for discovery again on that partial diff, not from scratch. Over time, the cost of keeping selectors current trends toward zero as layouts stabilize.

Most web scraping tools make you choose between cost and reliability. LLM-per-request APIs are accurate but expensive at scale. Regex heuristics are cheap but brittle. Yosoi takes a different approach: use an LLM once per domain to discover selectors, cache the result, and scrape indefinitely at near-zero cost.

## Technical stack

**Pydantic** [△](#ref-1) is the foundation for contract definitions and data validation. You define what you want to extract as a typed Pydantic model. Yosoi handles the rest.

**Async native.** The scraping pipeline is built on `asyncio` [○](#ref-2) from the ground up. `scrape()` is an async generator; `process_urls()` is fully non-blocking.

**Concurrent background workers.** `Pipeline.process_urls()` distributes work across a configurable worker pool. Discovery and extraction both run in parallel. A Rich [◑](#ref-3) Live progress table updates automatically when workers > 1.

## How it works

1. You provide a URL and a data contract (a typed Pydantic model describing what to extract)
2. Yosoi fetches the page HTML and sends it to an LLM
3. The LLM identifies stable CSS selectors for each field in the contract
4. Selectors are validated and stored in `.yosoi/selectors/`
5. Future scrapes use the cached selectors directly, with no LLM call needed

## FAQs

<details>
<summary>What is Yosoi?</summary>

**Y**ou **O**nly **S**crape **O**nce (**i**teratively). Instead of calling an LLM on every scrape or relying on flaky regex heuristics, Yosoi discovers selectors automatically the first time and caches them. You pay once and extract for free from then on. When selectors go stale, Yosoi re-discovers only the broken fields -- not the whole contract -- so costs stay minimal even as sites change.

</details>

<details>
<summary>How does Yosoi work?</summary>

You point it at a URL. Yosoi fetches the HTML, sends it to an LLM to identify stable CSS selectors, validates them, and caches the result. Every subsequent scrape of that domain uses the cached selectors directly with no LLM involved.

</details>

<details>
<summary>Why was Yosoi built?</summary>

For internal use at Cascading Labs. Every other API or LLM-per-request approach would have cost hundreds of thousands of dollars at scale. Yosoi was the only economically viable path, and we figured others had the same problem.

</details>

<details>
<summary>Does Yosoi work with JavaScript-rendered sites?</summary>

Yosoi fetches static HTML. For sites that require JavaScript to render content, use a headless browser (Playwright, Puppeteer) to render the page first, then pass the HTML to Yosoi. A native DOM fetcher is planned but not available yet.

</details>

<details>
<summary>What happens if a site redesigns its layout?</summary>

Some cached selectors will likely break. Yosoi detects stale selectors at scrape time and runs partial rediscovery -- only the broken fields are sent back to the LLM. The fresh selectors are merged into the existing cache. You can also force a full rediscovery by deleting the domain's file from `.yosoi/selectors/` or passing `--force`.

</details>

<details>
<summary>Which LLM provider gives the best results?</summary>

Results are generally consistent across providers. Groq and Gemini are fast and cheap; OpenAI tends to be more conservative with selector choices. Run discovery with `--model` to compare (e.g. `--model groq:llama-3.3-70b-versatile`).

</details>

## References

<a id="ref-1"></a>△ **Pydantic**. Pydantic Services Inc. *Data validation library for Python.* https://docs.pydantic.dev/

<a id="ref-2"></a>○ **asyncio**. Python Software Foundation. *Asynchronous I/O framework in the Python standard library.* https://docs.python.org/3/library/asyncio.html

<a id="ref-3"></a>◑ **Rich**. Will McGugan. *Python library for rich text and progress displays in the terminal.* https://rich.readthedocs.io/
