---
title: Roadmap
description: Planned features and future direction for Yosoi.
---

If something isn't shipped yet, you'll find it in one to three places:

1. **Here** -- on this page, as a planned item
2. **[GitHub Projects](https://github.com/orgs/CascadingLabs/projects)** -- for work that is actively planned or in progress
3. **[GitHub Issues](https://github.com/CascadingLabs/Yosoi/issues)** -- as a tracked issue in the Yosoi repo

If you want to follow progress on a specific feature, the GitHub issue is the most granular source. If you want a high-level picture of where the project is headed, start here.

---

## Proposed

### DOM-Enabled Scraping (A3Nodes)

A node-based pipeline architecture that would let Yosoi drive a real browser (Playwright [△](#ref-1)) to fetch and render JavaScript-heavy pages. L2 sites (SPAs, framework-rendered apps) would no longer require you to run Playwright yourself before passing HTML in.

The idea is to create a new class of selector that can capture DOM assertions, actions, and arrangements (A3) without needing an bulky LLM to drive.

Proposed node types:
- DOM fetcher: launches a browser, waits for network idle, captures the rendered DOM
- Authenticated fetcher: handles session cookies and login flows
- Proxy rotation: routes requests through a proxy pool
- Custom wait strategy: configurable DOM settling conditions for slow SPAs

Design is in progress. See [GitHub Projects](https://github.com/orgs/CascadingLabs/projects) for active planning.

---

## Planned

### QScrape L2 Sites

Fictional SPA test sites (React [○](#ref-2), Vue [◑](#ref-3), Svelte [◇](#ref-4), Lit [★](#ref-5)) for benchmarking a future DOM fetcher against known, stable targets. Mirrors the existing L1 suite.

### Distributed Selector Cache

Redis [⬡](#ref-6)-backed selector storage for teams sharing discovery results across machines and CI runs. See [Scaling](/guides/scaling/).

### Versioned Docs

Per-release documentation snapshots so older API versions remain accessible.

## References

<a id="ref-1"></a>△ **Playwright**. Microsoft. *Browser automation library for Node.js, Python, Java, and .NET.* https://playwright.dev/python/

<a id="ref-2"></a>○ **React**. Meta. *JavaScript library for building user interfaces.* https://react.dev/

<a id="ref-3"></a>◑ **Vue**. Evan You. *Progressive JavaScript framework for building UIs.* https://vuejs.org/

<a id="ref-4"></a>◇ **Svelte**. Rich Harris. *Compiler-based frontend framework.* https://svelte.dev/

<a id="ref-5"></a>★ **Lit**. Google. *Simple, fast web components library.* https://lit.dev/

<a id="ref-6"></a>⬡ **Redis**. Redis Ltd. *In-memory data structure store used as a database, cache, and message broker.* https://redis.io/docs/
