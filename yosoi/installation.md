---
title: Installation
description: How to install Yosoi and set up your environment.
---

Yosoi requires Python 3.10+ and uses uv<sup>[△](#ref-1)</sup> for package management.

## Install from PyPI

```bash
uv add yosoi
```

## Install from source

```bash
git clone https://github.com/CascadingLabs/Yosoi
cd Yosoi
uv sync
```

For development tools:

```bash
uv sync --group dev
```

## API keys

Create a `.env` file in your project root (see `env.example`):

```bash
# At least one provider is required
GROQ_KEY=your_groq_api_key
GEMINI_KEY=your_gemini_api_key
OPENAI_KEY=your_openai_api_key
CEREBRAS_KEY=your_cerebras_api_key
OPENROUTER_KEY=your_openrouter_api_key

# Optional: cloud observability via Logfire
LOGFIRE_TOKEN=your_logfire_token
```

Yosoi works with any of these providers<sup>[○](#ref-2)</sup><sup>[◑](#ref-3)</sup><sup>[◇](#ref-4)</sup><sup>[★](#ref-5)</sup><sup>[⬡](#ref-6)</sup>. You only need one. Set `LOGFIRE_TOKEN` to enable cloud observability via Logfire<sup>[▽](#ref-7)</sup>.

## FAQs

<details>
<summary>Can I use pip instead of uv?</summary>

Yes. `pip install yosoi` works fine. The docs use `uv` because it is faster and handles virtual environments automatically, but there is no hard dependency on it.

</details>

<details>
<summary>Do I need all of these API keys?</summary>

No. One is enough. Yosoi supports [25+ providers](/reference/helpers/) -- these five are just the most common. If multiple keys are present, set `YOSOI_MODEL` to specify which provider and model to use (e.g. `groq:llama-3.3-70b-versatile`).

</details>

<details>
<summary>Where should I put my .env file?</summary>

In your project root, next to `pyproject.toml`. Yosoi loads it automatically via `python-dotenv`<sup>[◎](#ref-8)</sup>. Do not commit it to version control.

</details>

<details>
<summary>What Python versions are supported?</summary>

Python 3.10 and above. Earlier versions are not supported due to use of modern type hint syntax.

</details>

## References

<a id="ref-1"></a>△ **uv**. Astral. *Python package and project manager.* https://docs.astral.sh/uv/

<a id="ref-2"></a>○ **Groq API**. Groq, Inc. *Low-latency LLM inference.* https://console.groq.com/docs/

<a id="ref-3"></a>◑ **Gemini API**. Google. *Gemini language model API.* https://ai.google.dev/gemini-api/docs

<a id="ref-4"></a>◇ **OpenAI API**. OpenAI. *GPT model API.* https://platform.openai.com/docs/

<a id="ref-5"></a>★ **Cerebras API**. Cerebras Systems. *High-speed LLM inference on wafer-scale hardware.* https://inference-docs.cerebras.ai/

<a id="ref-6"></a>⬡ **OpenRouter**. OpenRouter. *Unified API for LLM providers.* https://openrouter.ai/docs

<a id="ref-7"></a>▽ **Logfire**. Pydantic. *Cloud observability and tracing.* https://logfire.pydantic.dev/docs/

<a id="ref-8"></a>◎ **python-dotenv**. Saurabh Kumar. *Reads key-value pairs from a `.env` file and sets them as environment variables.* https://pypi.org/project/python-dotenv/
