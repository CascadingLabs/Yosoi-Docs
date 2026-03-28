---
title: JSON Output
description: Save Yosoi output to JSON.
---

```python
pipeline = ys.Pipeline(
    ys.auto_config(),
    contract=Article,
    output_format='json',
)
```

Results are written to `.yosoi/content/<domain>/results.json`.
