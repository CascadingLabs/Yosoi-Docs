---
title: Configuration
description: Environment variables and runtime options.
---


## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GROQ_KEY` | One of these | Groq API key |
| `GEMINI_KEY` | One of these | Google Gemini API key |
| `OPENAI_KEY` | One of these | OpenAI API key |
| `CEREBRAS_KEY` | One of these | Cerebras API key |
| `OPENROUTER_KEY` | One of these | OpenRouter API key |
| `LOGFIRE_TOKEN` | Optional | Enables Logfire tracing |

## Local storage

Yosoi stores all state in `.yosoi/` in your project root (gitignored by default):

```
.yosoi/
  selectors/     # Cached selector JSON per domain
  logs/          # Run logs (run_YYYYMMDD_HHMMSS.log)
  debug_html/    # Extracted HTML snapshots (--debug only)
```

## Observability

Set `LOGFIRE_TOKEN` to send traces to [Logfire](https://logfire.pydantic.dev) for cloud-based observability. Without it, logs are written locally only.
