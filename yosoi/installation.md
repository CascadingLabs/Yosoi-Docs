---
title: Installation
description: How to install Yosoi and set up your environment.
---


Yosoi requires Python 3.10+ and uses [uv](https://github.com/astral-sh/uv) for package management.

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

Yosoi works with any of these providers — you only need one.
