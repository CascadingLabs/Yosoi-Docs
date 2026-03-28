---
title: Provider Helpers
description: Provider helper reference for yosoi v0.0.1a11
---

> Generated from yosoi `v0.0.1a11`. Only symbols in `__all__` are listed.

## `alibaba` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L974" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`alibaba(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Alibaba Cloud DashScope.
**Args:**

- `model_name` `str` — DashScope model identifier (e.g. 'qwen-plus', 'qwen-max')
- `api_key` `str | None` — DashScope API key. If omitted, reads from DASHSCOPE_API_KEY or ALIBABA_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Alibaba DashScope.

## `anthropic` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L663" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`anthropic(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Anthropic (Claude).
**Args:**

- `model_name` `str` — Model identifier (e.g. 'claude-opus-4-5', 'claude-sonnet-4-6')
- `api_key` `str | None` — Anthropic API key. If omitted, reads from ANTHROPIC_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Anthropic.

## `azure` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L842" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`azure(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Azure OpenAI.

Supply ``azure_endpoint`` and optionally ``api_version`` via ``extra_params``.
**Args:**

- `model_name` `str` — Azure deployment name (e.g. 'gpt-4o')
- `api_key` `str | None` — Azure OpenAI API key. If omitted, reads from AZURE_OPENAI_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Azure OpenAI.

## `bedrock` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L774" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`bedrock(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for AWS Bedrock.

``api_key`` maps to ``aws_access_key_id``. Supply ``aws_secret_access_key``
and ``region_name`` via ``extra_params``, or let boto3 resolve credentials
from the environment.
**Args:**

- `model_name` `str` — Bedrock model ARN or ID (e.g. 'anthropic.claude-3-5-sonnet-20241022-v2:0')
- `api_key` `str | None` — AWS access key ID. If omitted, reads from AWS_ACCESS_KEY_ID.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for AWS Bedrock.

## `cerebras` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L725" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`cerebras(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Cerebras.
**Args:**

- `model_name` `str` — Cerebras model identifier (e.g. 'llama-3.3-70b')
- `api_key` `str | None` — Cerebras API key. If omitted, reads from CEREBRAS_API_KEY or CEREBRAS_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Cerebras.

## `deepseek` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L859" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`deepseek(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for DeepSeek.
**Args:**

- `model_name` `str` — DeepSeek model identifier (e.g. 'deepseek-chat', 'deepseek-reasoner')
- `api_key` `str | None` — DeepSeek API key. If omitted, reads from DEEPSEEK_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for DeepSeek.

## `fireworks` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L893" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`fireworks(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Fireworks AI.
**Args:**

- `model_name` `str` — Fireworks model identifier (e.g. 'accounts/fireworks/models/llama-v3p3-70b-instruct')
- `api_key` `str | None` — Fireworks API key. If omitted, reads from FIREWORKS_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Fireworks.

## `gemini` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L695" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`gemini(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Gemini (Google).
**Args:**

- `model_name` `str` — Gemini model identifier (e.g. 'gemini-2.0-flash')
- `api_key` `str | None` — Google API key. If omitted, reads from GEMINI_API_KEY, GEMINI_KEY, or GOOGLE_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Gemini.

## `github` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1023" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`github(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for GitHub Models.
**Args:**

- `model_name` `str` — GitHub Models identifier (e.g. 'gpt-4o', 'Llama-3.3-70B-Instruct')
- `api_key` `str | None` — GitHub token. If omitted, reads from GITHUB_TOKEN.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for GitHub Models.

## `grok` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L959" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`grok(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Grok via xAI's OpenAI-compatible endpoint.
**Args:**

- `model_name` `str` — Grok model identifier (e.g. 'grok-3', 'grok-3-mini')
- `api_key` `str | None` — xAI API key. If omitted, reads from XAI_API_KEY or GROK_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Grok.

## `groq` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L680" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`groq(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Groq.
**Args:**

- `model_name` `str` — Groq model identifier (e.g. 'llama-3.3-70b-versatile')
- `api_key` `str | None` — Groq API key. If omitted, reads from GROQ_API_KEY or GROQ_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Groq.

## `heroku` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1053" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`heroku(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Heroku Managed Inference.
**Args:**

- `model_name` `str` — Heroku model identifier (e.g. 'claude-3-5-sonnet')
- `api_key` `str | None` — Heroku inference key. If omitted, reads from HEROKU_INFERENCE_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Heroku.

## `huggingface` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L742" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`huggingface(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for HuggingFace Inference API.
**Args:**

- `model_name` `str` — HuggingFace model ID (e.g. 'Qwen/Qwen3-235B-A22B')
- `api_key` `str | None` — HF token. If omitted, reads from HF_TOKEN or HUGGINGFACE_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields (e.g. extra_params={'provider_name': 'nebius'}).

**Returns:** `LLMConfig` — Configured LLMConfig for HuggingFace.

## `litellm` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1068" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`litellm(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for LiteLLM proxy.

Supply ``api_base`` via ``extra_params`` to point at your LiteLLM proxy
endpoint.
**Args:**

- `model_name` `str` — Model identifier passed through to LiteLLM
- `api_key` `str | None` — API key for the proxied provider. If omitted, reads from LITELLM_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for LiteLLM.

## `mistral` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L710" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`mistral(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Mistral.
**Args:**

- `model_name` `str` — Mistral model identifier (e.g. 'mistral-large-latest')
- `api_key` `str | None` — Mistral API key. If omitted, reads from MISTRAL_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Mistral.

## `moonshotai` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L942" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`moonshotai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for MoonshotAI (Kimi).
**Args:**

- `model_name` `str` — Moonshot model identifier (e.g. 'kimi-k2-0711-preview')
- `api_key` `str | None` — Moonshot API key. If omitted, reads from MOONSHOT_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for MoonshotAI.

## `nebius` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L927" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`nebius(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Nebius AI Studio.
**Args:**

- `model_name` `str` — Nebius model identifier (e.g. 'Qwen/Qwen3-235B-A22B-fast')
- `api_key` `str | None` — Nebius API key. If omitted, reads from NEBIUS_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Nebius.

## `ollama` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L876" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`ollama(model_name: str, kwargs: Any = {}) -> LLMConfig`

Quick config for Ollama (local).

No API key required. Supply ``base_url`` via ``extra_params`` to override
the default ``http://localhost:11434``.
**Args:**

- `model_name` `str` — Ollama model tag (e.g. 'llama3', 'mistral', 'qwen2.5')
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Ollama.

## `openai` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L810" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`openai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OpenAI.
**Args:**

- `model_name` `str` — OpenAI model identifier (e.g. 'gpt-4o', 'gpt-4o-mini')
- `api_key` `str | None` — OpenAI API key. If omitted, reads from OPENAI_API_KEY or OPENAI_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OpenAI.

## `openrouter` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L825" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`openrouter(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OpenRouter.
**Args:**

- `model_name` `str` — OpenRouter model identifier (e.g. 'meta-llama/llama-3.3-70b-instruct:free')
- `api_key` `str | None` — OpenRouter API key. If omitted, reads from OPENROUTER_API_KEY or OPENROUTER_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OpenRouter.

## `ovhcloud` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1006" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`ovhcloud(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OVHcloud AI Endpoints.
**Args:**

- `model_name` `str` — OVHcloud model identifier
- `api_key` `str | None` — OVH access token. If omitted, reads from OVH_AI_ENDPOINTS_ACCESS_TOKEN.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OVHcloud.

## `provider` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1138" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`provider(model_string: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Create an LLM config from a single model string.

This is the recommended, unified way to configure a model.  The provider is
parsed from the model string automatically.

Preferred format uses ``:`` as the separator::

    import yosoi as ys

    config = ys.provider('groq:llama-3.3-70b-versatile')
    config = ys.provider('openrouter:meta-llama/llama-3.3-70b-instruct:free')
    config = ys.provider('gemini:gemini-2.0-flash')
    config = ys.provider('anthropic:claude-opus-4-5')
    config = ys.provider('deepseek:deepseek-chat')
    config = ys.provider('ollama:llama3')

The ``provider/model`` format is also supported for known providers::

    config = ys.provider('groq/llama-3.3-70b-versatile')
**Args:**

- `model_string` `str` — Model identifier in ``provider:model-name`` format.
- `api_key` `str | None` — Explicit API key. If omitted, resolved from environment.
- `**kwargs` `Any` — Additional LLMConfig fields (temperature, max_tokens, etc.)

**Returns:** `LLMConfig` — Configured LLMConfig instance.

**Raises:**

- `ValueError` — If the provider cannot be determined.

## `sambanova` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L989" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`sambanova(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for SambaNova.
**Args:**

- `model_name` `str` — SambaNova model identifier (e.g. 'Meta-Llama-3.3-70B-Instruct')
- `api_key` `str | None` — SambaNova API key. If omitted, reads from SAMBANOVA_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for SambaNova.

## `together` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L910" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`together(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Together AI.
**Args:**

- `model_name` `str` — Together model identifier (e.g. 'meta-llama/Llama-3-70b-chat-hf')
- `api_key` `str | None` — Together API key. If omitted, reads from TOGETHER_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Together AI.

## `vercel` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L1038" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`vercel(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Vercel AI.
**Args:**

- `model_name` `str` — Vercel AI model identifier
- `api_key` `str | None` — Vercel API key. If omitted, reads from AI_SDK_KEY or VERCEL_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Vercel AI.

## `vertexai` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L793" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`vertexai(model_name: str, kwargs: Any = {}) -> LLMConfig`

Quick config for Google Vertex AI.

No API key required — uses GCP application default credentials or a
service account file supplied via ``extra_params``.
**Args:**

- `model_name` `str` — Vertex AI model ID (e.g. 'gemini-2.0-flash-001')
- `**kwargs` `Any` — Additional LLMConfig fields (e.g. extra_params={'project_id': '...', 'region': 'us-east1'}).

**Returns:** `LLMConfig` — Configured LLMConfig for Google Vertex AI.

## `xai` <a href="https://github.com/CascadingLabs/Yosoi/blob/0.0.1a11/yosoi/core/discovery/config.py#L759" target="_blank" rel="noopener noreferrer" title="View source on GitHub"><svg aria-hidden="true" height="14" viewBox="0 0 16 16" version="1.1" width="14" xmlns="http://www.w3.org/2000/svg" style="vertical-align:-2px;display:inline-block"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/></svg></a>

`xai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for xAI (Grok models via native xAI client).
**Args:**

- `model_name` `str` — xAI model identifier (e.g. 'grok-3', 'grok-3-mini')
- `api_key` `str | None` — xAI API key. If omitted, reads from XAI_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for xAI.

