---
title: News Portal
description: Extract articles from a news portal using Yosoi.
---

Target: [Mountainhome Herald](https://qscrape.dev/l1/news) (QScrape L1)

```python
import asyncio
import yosoi as ys

class Article(ys.Contract):
    title: str = ys.Title()
    author: str = ys.Author()
    date: str = ys.Datetime()
    url: str = ys.Url()

async def main():
    pipeline = ys.Pipeline(ys.auto_config(), contract=Article)

    async for item in pipeline.scrape('https://qscrape.dev/l1/news'):
        print(item.get('title'), item.get('author'))

asyncio.run(main())
```
