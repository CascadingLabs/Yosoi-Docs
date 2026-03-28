---
title: Roadmap
description: Planned features and future direction for Yosoi.
---

If something isn't shipped yet, you'll find it in one of two places:

1. **Here** -- on this page, as a major planned item
3. **[GitHub Issues](https://github.com/CascadingLabs/Yosoi/issues)** -- as a tracked issue in the Yosoi repo

If you want to follow progress on a specific feature, the GitHub issue is the most granular source. If you want a high-level picture of where the project is headed, start here.

---

## Planned

### QScrape L2 Sites

Fictional SPA test sites (React<sup>[○](#ref-2)</sup>, Vue<sup>[◑](#ref-3)</sup>, Svelte<sup>[◇](#ref-4)</sup>, Lit<sup>[★](#ref-5)</sup>) for benchmarking a future DOM fetcher against known, stable targets. Mirrors the existing L1 suite.

### Distributed Selector Cache

Redis<sup>[⬡](#ref-6)</sup> and Turso<sup>[◎](#ref-7)</sup>-backed selector storage for teams sharing discovery results across machines and CI runs. See [Scaling](/guides/scaling/).

### Versioned Docs

Per-release documentation snapshots so older API versions remain accessible.

### Conda Forge Distribution

Publish Yosoi to Conda Forge to make installation as easy as possible for users in the conda ecosystem.

Issue: [#56](https://github.com/CascadingLabs/Yosoi/issues/56)

## Proposed

### DOM-Enabled Scraping (A3Nodes)

A DAG and node-based pipeline architecture that would let Yosoi drive a real browser (Zendriver<sup>[△](#ref-1)</sup>) to fetch and render JavaScript-heavy pages. L2 sites (SPAs, framework-rendered apps) would no longer require you to run a browser automation tool yourself before passing HTML in.

The idea is to create a new class of selector that can capture DOM assertions, actions, and arrangements (A3) without needing a bulky LLM to drive.

### Canonicalization Engine

A mode that merges selector caches across domains that serve the same content. If two sources (e.g. thewallstreetjournal.com and wsj.com) publish equivalent data, enabling canonicalization on a contract would collapse them into a single canonical selector set. Reducing redundant discovery and keeping extraction consistent. Implementation would likely involve tracing or logging logic to detect overlapping field mappings, then coercing the duplicate into the canonical domain's cache. May warrant a separate repo/package.

Issue: [#39](https://github.com/CascadingLabs/Yosoi/issues/39)

### Super Crawler

A first-class multi-page crawling mode. Currently Yosoi operates on single pages — there is no way to chain together multiple linked pages. Multi-page crawling is a common use-case that makes sense to include natively. This would likely require expanding the AI generation step so that stateful "steps" are defined for the LLM to replay its predecessor's selectors and JavaScript actions needed to complete a crawl. Much of this will be blocked by JS rendering and execution, tying it closely to the DOM-Enabled Scraping (A3Nodes) proposal above.

Issue: [#34](https://github.com/CascadingLabs/Yosoi/issues/34)

### Smart Batching of Tokens

Currently the pipeline sends N requests (one per contract field), each containing the full HTML, and hopes the LLM's context window is large enough. This needs to be more defensive. A smart batching or context management system would use a lightweight lxml pre-processor to trim the HTML to a safe-enough, close-enough subset per contract — reducing token cost and avoiding context window overflows.

Issue: [#50](https://github.com/CascadingLabs/Yosoi/issues/50)

### Dynamic Schema Builder

A JSON codegen tool that lets users define a schema in JSON and generates a Pydantic contract from it. This lowers the barrier for newcomers who find OOP-style contract definitions (`ys.Contract`) intimidating but still need the specificity that Pydantic models provide for structured LLM output. Useful for REST and MCP design workflows as well. The `Prompt → Contract → Selectors → Content` pipeline would gain a new entry point.

Issue: [#33](https://github.com/CascadingLabs/Yosoi/issues/33)

### Custom Yosoi SLMs

Custom Small Language Model for fully offline private scraping ≤ 3 billion parameters.

## References

<a id="ref-1"></a>△ **Zendriver**. cdpdriver. *Python-based browser automation using the Chrome DevTools Protocol.* https://github.com/cdpdriver/zendriver

<a id="ref-2"></a>○ **React**. Meta. *JavaScript library for building user interfaces.* https://react.dev/

<a id="ref-3"></a>◑ **Vue**. Evan You. *Progressive JavaScript framework for building UIs.* https://vuejs.org/

<a id="ref-4"></a>◇ **Svelte**. Rich Harris. *Compiler-based frontend framework.* https://svelte.dev/

<a id="ref-5"></a>★ **Lit**. Google. *Simple, fast web components library.* https://lit.dev/

<a id="ref-6"></a>⬡ **Redis**. Redis Ltd. *In-memory data structure store used as a database, cache, and message broker.* https://redis.io/docs/

<a id="ref-7"></a>◎ **Turso**. Turso. *Edge-hosted distributed SQLite database.* https://turso.tech/
