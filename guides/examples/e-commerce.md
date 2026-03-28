---
title: E-Commerce Catalogue
description: Extract products from an e-commerce catalogue using Yosoi.
---

Target: [VaultMart](https://qscrape.dev/l1/eshop) (QScrape L1)

```python
import asyncio
import yosoi as ys

class Product(ys.Contract):
    root = ys.css('article.product')

    name: str = ys.Title()
    price: float = ys.Price()
    rating: str = ys.Rating()

async def main():
    pipeline = ys.Pipeline(ys.auto_config(), contract=Product)

    async for item in pipeline.scrape('https://qscrape.dev/l1/eshop'):
        print(item.get('name'), item.get('price'))

asyncio.run(main())
```
