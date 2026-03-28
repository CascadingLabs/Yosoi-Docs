---
title: Configuration
description: Environment variables and runtime options.
---

## Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GROQ_KEY` | One of these | Groq<sup>[△](#ref-1)</sup> API key |
| `GEMINI_KEY` | One of these | Google Gemini<sup>[○](#ref-2)</sup> API key |
| `OPENAI_KEY` | One of these | OpenAI<sup>[◑](#ref-3)</sup> API key |
| `CEREBRAS_KEY` | One of these | Cerebras<sup>[◇](#ref-4)</sup> API key |
| `OPENROUTER_KEY` | One of these | OpenRouter<sup>[★](#ref-5)</sup> API key |
| `YOSOI_MODEL` | Optional | Default model in `provider:model` format (e.g. `groq:llama-3.3-70b-versatile`) |
| `YOSOI_LOG_LEVEL` | Optional | Logging level: `DEBUG`, `INFO`, `WARNING`, `ERROR`, `ALL` (default: `DEBUG`) |
| `LOGFIRE_TOKEN` | Optional | Enables Logfire<sup>[⬡](#ref-6)</sup> tracing |

These are the most commonly used provider keys. Yosoi supports [25+ providers](/reference/helpers/) -- each with its own environment variable. You only need one.

## Local storage

Yosoi stores all state in `.yosoi/` in your project root (gitignored by default):

```
.yosoi/
  selectors/     # Cached selector JSON per domain
  logs/          # Run logs (run_YYYYMMDD_HHMMSS.log)
  debug_html/    # Extracted HTML snapshots (--debug only)
  content/       # Extracted output files (JSON, CSV, etc.)
  stats.json     # Cumulative LLM call and usage statistics
```

## Observability

Set `LOGFIRE_TOKEN` to send traces to [Logfire](https://logfire.pydantic.dev) for cloud-based observability. Without it, logs are written locally only.

## FAQs

<details>
<summary>What happens if I set multiple provider keys?</summary>

Yosoi picks one based on a built-in fallback order (Groq, Gemini, Cerebras, OpenAI, OpenRouter). To control which provider and model are used, set `YOSOI_MODEL` to a `provider:model` string (e.g. `groq:llama-3.3-70b-versatile`).

</details>

<details>
<summary>Can I change the .yosoi/ storage location?</summary>

Not currently. The directory is always created in the working directory where Yosoi is run.

</details>

<details>
<summary>Is .yosoi/ safe to commit to version control?</summary>

The selector cache is safe to commit if you want to share discovered selectors across a team. The `logs/`, `debug_html/`, and `content/` subdirectories are noisy and should stay gitignored.

</details>

<details>
<summary>How do I enable debug HTML snapshots?</summary>

Pass `--debug` when running the CLI. Snapshots are saved to `.yosoi/debug_html/` and are useful for diagnosing extraction failures.

</details>

## References

<a id="ref-1"></a>△ **Groq API**. Groq, Inc. *Low-latency LLM inference.* https://console.groq.com/docs/

<a id="ref-2"></a>○ **Gemini API**. Google. *Gemini language model API.* https://ai.google.dev/gemini-api/docs

<a id="ref-3"></a>◑ **OpenAI API**. OpenAI. *GPT model API.* https://platform.openai.com/docs/

<a id="ref-4"></a>◇ **Cerebras API**. Cerebras Systems. *High-speed LLM inference on wafer-scale hardware.* https://inference-docs.cerebras.ai/

<a id="ref-5"></a>★ **OpenRouter**. OpenRouter. *Unified API for LLM providers.* https://openrouter.ai/docs

<a id="ref-6"></a>⬡ **Logfire**. Pydantic. *Cloud observability and tracing.* https://logfire.pydantic.dev/docs/
