---
title: Understanding the Web
description: How HTML, the DOM, and JavaScript frameworks affect what Yosoi can see and extract.
---

Not all websites are equally easy to scrape. Understanding why helps you choose the right approach and set realistic expectations before discovery runs.

## HTML vs. the DOM

When you load a page in a browser, the browser parses the raw HTML and constructs a live tree of objects called the DOM [△](#ref-1) (Document Object Model). JavaScript can then modify that tree: adding nodes, removing them, rewriting text content, injecting entire components. What you see on screen may look nothing like the original HTML the server sent.

Yosoi fetches the raw HTML. It sees what the server returns, not what JavaScript builds after the fact. For most news sites, blogs, and product catalogues this is fine. The content is in the HTML. For single-page apps that load data after the initial render, Yosoi will get a mostly-empty shell.

If you can view the page source in your browser (`Cmd+U` / `Ctrl+U`) and see the text you want to extract, Yosoi can work with it. If the content only appears after JavaScript runs, render the page yourself with Playwright [○](#ref-2) or Puppeteer [◑](#ref-3) and pass the HTML to Yosoi directly.

A native DOM fetcher that handles this automatically is on the [Roadmap](/roadmap/), but is not available yet.

## Difficulty levels

### L1: Static HTML, CSS, and JS

Standard HTML pages with no frontend framework and no dynamic data loading. The full content is present in the server response. Selectors are stable and discovery is reliable.

These are the easiest targets. [QScrape L1 sites](https://qscrape.dev) simulate this category with realistic content and layouts.

### L2: SPAs and data-driven dynamic sites

Single-page applications and sites that load content after the initial HTML render. The server sends a minimal shell; JavaScript fetches data and injects it into the DOM. By the time the page looks right in a browser, the raw HTML Yosoi fetched may be largely empty.

For L2 sites, render the page yourself with a headless browser (Playwright [○](#ref-2), Puppeteer [◑](#ref-3)) and pass the resulting HTML to Yosoi. Discovery works against the rendered output the same way it works against static HTML.

[QScrape L2 sites](https://qscrape.dev) cover this category with Lit [◇](#ref-4), Svelte [★](#ref-5), React [⬡](#ref-6), and Vue [▽](#ref-7).

### L3: Anti-bot sites

Sites that actively try to detect and block automated access. Techniques include rate limiting, fingerprinting request headers, requiring session cookies, obfuscating markup, and serving different content to suspected bots.

Yosoi does not attempt to bypass anti-bot measures. If a site blocks the HTTP request, discovery fails. You are responsible for handling authentication, headers, and session management before passing HTML to Yosoi.

[QScrape L3 sites](https://qscrape.dev) apply generic anti-bot patterns (excluding captchas) for testing.

### L4: Captchas and traffic monitoring

The hardest class of sites. In addition to L3 protections, these deploy active challenge puzzles (CAPTCHAs, proof-of-work) and monitor traffic patterns across sessions to flag and block suspicious behavior.

Bypassing L4 protections is outside Yosoi's scope. Anti-captcha APIs and residential proxy networks exist for this purpose but are not integrated. QScrape does not include L4 sites.

## QScrape

[QScrape](https://qscrape.dev) is a purpose-built evaluation suite of fictional websites across the three difficulty levels above. Use it to:

- Validate that Yosoi's selector discovery works correctly for a given site type
- Regression-test your pipelines against a stable, unchanging source
- Benchmark discovery accuracy across providers

Because QScrape sites are controlled and stable, they are ideal for CI. Point Yosoi at a QScrape URL and assert on the extracted field values.

## FAQs

<details>
<summary>Can Yosoi scrape single-page apps (L2 sites)?</summary>

Not directly. Yosoi fetches raw HTML, which is mostly empty for SPAs. Render the page yourself with a headless browser (Playwright, Puppeteer) and pass the rendered HTML to Yosoi. A native DOM fetcher is on the [Roadmap](/roadmap/) but not available yet.

</details>

<details>
<summary>Why do class names change between deploys on framework-based sites?</summary>

Build tools like webpack [◎](#ref-8) and Vite [✦](#ref-9) generate hashed class names to enable long-term caching. A deploy changes the hash, which invalidates any selector that targets that class. Yosoi's LLM-based discovery tries to avoid these by preferring stable attributes (IDs, data attributes, semantic tags), but it is not guaranteed.

</details>

<details>
<summary>What is the practical difference between L2 and L3 difficulty?</summary>

L2 adds frontend framework complexity but does not try to block you. L3 actively resists scraping. A tool that works on L2 will not necessarily work on L3.

</details>

<details>
<summary>Should I test against QScrape sites before hitting my real targets?</summary>

Yes. It is a fast way to verify your pipeline is wired up correctly before sending requests to sites you do not control.

</details>

## References

<a id="ref-1"></a>△ **DOM (Document Object Model)**. W3C / MDN. *Programmatic interface for HTML and XML documents, representing the page as a tree of objects.* https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model

<a id="ref-2"></a>○ **Playwright**. Microsoft. *Browser automation library for Node.js, Python, Java, and .NET.* https://playwright.dev/python/

<a id="ref-3"></a>◑ **Puppeteer**. Google Chrome DevTools. *Node.js library providing a high-level API to control headless Chrome.* https://pptr.dev/

<a id="ref-4"></a>◇ **Lit**. Google. *Simple, fast, web components library.* https://lit.dev/

<a id="ref-5"></a>★ **Svelte**. Rich Harris. *Compiler-based frontend framework.* https://svelte.dev/

<a id="ref-6"></a>⬡ **React**. Meta. *JavaScript library for building user interfaces.* https://react.dev/

<a id="ref-7"></a>▽ **Vue**. Evan You. *Progressive JavaScript framework for building UIs.* https://vuejs.org/

<a id="ref-8"></a>◎ **webpack**. webpack contributors. *Static module bundler for JavaScript applications.* https://webpack.js.org/

<a id="ref-9"></a>✦ **Vite**. Evan You. *Next generation frontend build tool.* https://vite.dev/
