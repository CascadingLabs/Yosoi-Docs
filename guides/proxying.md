---
title: Proxying
description: Using proxies with Yosoi for distributed scraping.
---

*Full documentation coming soon.*

## A note on responsible use

Yosoi is designed for respectful scraping. When routing requests through proxies, please do not use TOR [△](#ref-1) exit nodes or public SOCKS5 [○](#ref-2) servers. These are shared public IP systems; using them for scraping loads volunteer-run infrastructure with automated traffic it was not designed to carry, and it degrades the experience for everyone who relies on those networks for legitimate privacy use.

If you need to route requests through multiple IPs, use dedicated residential or datacenter proxies from providers that explicitly offer them for this purpose.

## References

<a id="ref-1"></a>△ **Tor Project**. The Tor Project. *Free, open-source software enabling anonymous communication online.* https://www.torproject.org/

<a id="ref-2"></a>○ **SOCKS5**. IETF RFC 1928. *Protocol for routing network packets between a client and server through a proxy.* https://datatracker.ietf.org/doc/html/rfc1928
