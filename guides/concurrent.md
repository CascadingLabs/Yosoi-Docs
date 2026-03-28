---
title: Concurrent Scraping
description: Process multiple URLs in parallel with the Pipeline.
---

`Pipeline.process_urls()` accepts a list of URLs and a `workers` argument. When `workers > 1`, a Rich<sup>[△](#ref-1)</sup> Live progress table appears automatically. No extra setup required.

## Basic usage

```python
import asyncio
import yosoi as ys
from yosoi import Pipeline
from yosoi.utils.files import init_yosoi, is_initialized

URLS = [
    'https://news.ycombinator.com',
    'https://lobste.rs',
    'https://thenewstack.io',
]

async def main() -> None:
    if not is_initialized():
        init_yosoi()

    config = ys.auto_config()  # picks up YOSOI_MODEL / provider keys from .env
    pipeline = Pipeline(config, contract=ys.NewsArticle)

    results = await pipeline.process_urls(URLS, workers=3)
    print(f'Done: {len(results["successful"])} succeeded, {len(results["failed"])} failed')

asyncio.run(main())
```

## Result shape

`process_urls()` returns a dict with three keys:

| Key | Value |
|-----|-------|
| `successful` | List of URLs that completed without error |
| `failed` | List of URLs that raised an exception |
| `skipped` | List of URLs that were skipped (concurrent mode only) |

## Notes

- Selector discovery (the one-time LLM call) is also parallelised across workers.
- Cached domains skip discovery entirely; only extraction runs.
- `workers=1` (the default) runs sequentially with no progress table.

## FAQs

<details>
<summary>How many workers should I use?</summary>

Start with 3 to 5. Higher counts can trigger rate limiting from both the target site and your LLM provider. The right number depends on your provider's rate limits and the target site's tolerance.

</details>

<details>
<summary>What happens if one URL fails?</summary>

It is added to the `failed` list and the rest continue. Exceptions are caught per-URL and do not abort the batch.

</details>

<details>
<summary>Does concurrency affect selector discovery?</summary>

Yes, in a good way. If multiple URLs share a domain that has not been discovered yet, one worker runs discovery while the others wait. Once cached, all workers use the result.

</details>

<details>
<summary>Can I retry failed URLs automatically?</summary>

Not built-in. After `process_urls()` returns, pass `results["failed"]` back into another `process_urls()` call to retry.

</details>

## References

<a id="ref-1"></a>△ **Rich**. Will McGugan. *Python library for rich text and progress displays in the terminal.* https://rich.readthedocs.io/

<a id="ref-2"></a>○ **asyncio**. Python Software Foundation. *Asynchronous I/O framework in the Python standard library.* https://docs.python.org/3/library/asyncio.html
