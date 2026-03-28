---
title: Sports Scores
description: Extract sports scores using Yosoi.
---

Target: [ScoreTap](https://qscrape.dev/l1/scoretap) (QScrape L1)

```python
import asyncio
import yosoi as ys

class Match(ys.Contract):
    root = ys.css('div.match-row')

    teams: str = ys.Field(description='Team names')
    score: str = ys.Field(description='Final score')
    date: str = ys.Datetime()

async def main():
    pipeline = ys.Pipeline(ys.auto_config(), contract=Match)

    async for item in pipeline.scrape('https://qscrape.dev/l1/scoretap'):
        print(item.get('teams'), item.get('score'))

asyncio.run(main())
```
