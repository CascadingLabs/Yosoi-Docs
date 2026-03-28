---
title: Concurrent Scraping
description: Scrape multiple sites concurrently with Yosoi.
---

```python
import asyncio
import yosoi as ys
from yosoi import Pipeline
from yosoi.utils.files import init_yosoi, is_initialized

URLS = [
    'https://qscrape.dev/l1/news',
    'https://qscrape.dev/l1/scoretap',
    'https://qscrape.dev/l1/eshop',
]

async def main():
    if not is_initialized():
        init_yosoi()

    pipeline = Pipeline(ys.auto_config(), contract=ys.NewsArticle)
    results = await pipeline.process_urls(URLS, workers=3)

    print(f'{len(results["successful"])} succeeded, {len(results["failed"])} failed')

asyncio.run(main())
```
