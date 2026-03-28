---
title: API Reference
description: Full API reference for yosoi v0.0.1a11
version: v0.0.1a11
---


> Generated from yosoi `v0.0.1a11`. Only symbols in `__all__` are listed.

## Classes

### `Contract`

Base class for user-defined scraping contracts.

#### `define`

`define(name: str) -> ContractBuilder`

Start a fluent ContractBuilder for the given contract name.

#### `discovery_field_names`

`discovery_field_names() -> set[str]`

Return the set of flattened field names used for discovery and cache keys.

Non-Contract fields keep their original name; nested Contract fields are
expanded to ``{parent}_{child}`` keys.  This matches the key format used
by snapshots, ``field_descriptions()``, and ``get_selector_overrides()``.

#### `field_descriptions`

`field_descriptions() -> dict[str, str]`

Return a mapping of field name to description, excluding selector overrides.

Nested Contract-typed fields are expanded to flat ``{parent}_{child}`` keys.
When the child contract has a pinned root, the description includes a scoping hint.
When the child has ``root = ys.discover()``, a co-location hint is added.

#### `field_hints`

`field_hints() -> dict[str, str | None]`

Return yosoi_hint per (flat) field name, expanding nested contracts to {parent}_{child}.

#### `generate_manifest`

`generate_manifest() -> str`

Return a markdown table documenting all contract fields and their config.

#### `get_root`

`get_root() -> SelectorEntry | None`

Return the root selector if explicitly set on the contract class.
**Returns:** `SelectorEntry | None` — SelectorEntry for the repeating container element, or None.

#### `get_selector_overrides`

`get_selector_overrides() -> dict[str, dict[str, str]]`

Return selector overrides defined on fields via ``yosoi_selector``.
**Returns:** `dict[str, dict[str, str]]` — Mapping of field name → selector dict (compatible with ``FieldSelectors`` `dict[str, dict[str, str]]` — structure, e.g. ``{"primary": "h1.title"}``). `dict[str, dict[str, str]]` — Nested contract overrides are included as flat ``{parent}_{child}`` keys.

#### `is_grouped`

`is_grouped() -> bool`

Return True if the contract explicitly configures multi-item mode.

#### `list_fields`

`list_fields() -> dict[str, type]`

Return {field_name: inner_type} for fields annotated as list[T].

#### `nested_contracts`

`nested_contracts() -> dict[str, type[Contract]]`

Return a mapping of field name → child Contract class for Contract-typed fields.

#### `to_selector_model`

`to_selector_model() -> type[BaseModel]`

Generate a Pydantic model mapping each contract field to FieldSelectors.

This ensures that the LLM agent knows exactly which fields to find selectors for,
preserving any descriptions or hints provided in the contract.
Fields with a ``yosoi_selector`` override are excluded — their selectors are
provided directly and do not require AI discovery.
Nested Contract-typed fields are expanded to flat ``{parent}_{child}`` entries.

### `DebugConfig`

Configuration for debug output.

### `JobPosting`

Contract for job listing pages.

### `LLMConfig`

Base configuration for any LLM provider.

### `NewsArticle`

Default contract matching the original 5-field behavior.

### `Pipeline`

Main pipeline for discovering and saving CSS selectors with retry logic.

The main pipeline of YOSOi that goes through all the other python files to
fetch the HTML, parse the HTML, have an LLM discover the selectors, and
verify and store the selectors.

#### `normalize_url`

`normalize_url(url: str) -> str`

Add protocol to URL, preferring https.
**Args:**

- `url` `str` — The URL that is being fetched

**Returns:** `str` — The complete URL

#### `process_url`

`process_url(url: str, force: bool | None = None, max_fetch_retries: int = 2, max_discovery_retries: int = 3, skip_verification: bool = False, fetcher_type: str = 'simple', output_format: str | list[str] | None = None) -> None`

Process a single URL: discover, verify, and save selectors.

Thin wrapper around :meth:`scrape` that drains the generator.
Raises on failure — callers are responsible for error handling.
**Args:**

- `url` `str` — URL to process
- `force` `bool | None` — Force re-discovery even if selectors exist. Defaults to False.
- `skip_verification` `bool` — Skip verification step. Defaults to False.
- `fetcher_type` `str` — Type of fetcher ('simple'). Defaults to 'simple'.
- `max_fetch_retries` `int` — Maximum fetch retry attempts. Defaults to 2.
- `max_discovery_retries` `int` — Maximum AI discovery retry attempts. Defaults to 3.
- `output_format` `str | list[str] | None` — Format(s) for extracted content. Defaults to None (uses pipeline default).

#### `process_urls`

`process_urls(urls: list[str], force: bool | None = None, skip_verification: bool = False, fetcher_type: str = 'simple', max_fetch_retries: int = 2, max_discovery_retries: int = 3, output_format: str | list[str] | None = None, workers: int = 1, on_complete: Callable[[str, bool, float], Awaitable[None]] | None = None, on_start: Callable[[str], Awaitable[None]] | None = None) -> dict[str, list[str]]`

Process multiple URLs and collect results.

When ``workers`` > 1 and there are multiple URLs, processing runs
concurrently via the taskiq broker.  Otherwise URLs are processed
sequentially.
**Args:**

- `urls` `list[str]` — List of URLs to process.
- `force` `bool | None` — Force re-discovery even if selectors exist. Defaults to False.
- `skip_verification` `bool` — Skip verification step. Defaults to False.
- `fetcher_type` `str` — Type of fetcher ('simple'). Defaults to 'simple'.
- `max_fetch_retries` `int` — Maximum fetch retry attempts. Defaults to 2.
- `max_discovery_retries` `int` — Maximum AI discovery retry attempts. Defaults to 3.
- `output_format` `str | list[str] | None` — Format(s) for extracted content. Defaults to None (uses pipeline default).
- `workers` `int` — Number of concurrent workers. Defaults to 1 (sequential).
- `on_complete` `Callable[[str, bool, float], Awaitable[None]] | None` — Optional async callback ``(url, success, elapsed)`` called
after each URL finishes. Used by the CLI for live progress display.
- `on_start` `Callable[[str], Awaitable[None]] | None` — Optional async callback ``(url)`` called just before each
URL begins processing.

**Returns:** `dict[str, list[str]]` — Dictionary with keys:
- 'successful': List of successfully processed URLs
- 'failed': List of URLs that failed processing
- 'skipped': List of URLs skipped (concurrent only)

#### `scrape`

`scrape(url: str, force: bool | None = None, max_fetch_retries: int = 2, max_discovery_retries: int = 3, skip_verification: bool = False, fetcher_type: str = 'simple', output_format: str | list[str] | None = None) -> AsyncIterator[ContentMap]`

Async generator yielding individual content items from a URL.

Canonical entry point — handles both cached-selector replay and fresh
AI discovery.  For multi-item pages (catalogs, listings), yields one
``ContentMap`` per matched container element.  For single-item pages,
yields exactly one ``ContentMap``.
**Args:**

- `url` `str` — URL to process
- `force` `bool | None` — Force re-discovery even if selectors exist. Defaults to
the pipeline-level ``force`` flag.
- `max_fetch_retries` `int` — Maximum fetch retry attempts. Defaults to 2.
- `max_discovery_retries` `int` — Maximum AI discovery retry attempts. Defaults to 3.
- `skip_verification` `bool` — Skip verification step. Defaults to False.
- `fetcher_type` `str` — Type of fetcher ('simple'). Defaults to 'simple'.
- `output_format` `str | list[str] | None` — Format(s) for saving extracted content.

**Yields:** `AsyncIterator[ContentMap]` — ContentMap dicts — one per extracted item.

#### `show_llm_stats`

`show_llm_stats() -> None`

Show LLM usage statistics.

#### `show_summary`

`show_summary() -> None`

Show summary of all saved selectors.

### `SelectorEntry`

A single selector with its strategy and value.

### `TelemetryConfig`

Configuration for observability / telemetry.

### `Video`

Contract for video pages (YouTube-style).

### `YosoiConfig`

Top-level Yosoi configuration bundling LLM, debug, and telemetry settings.

Example::

    config = YosoiConfig(
        llm=ys.groq('llama-3.3-70b-versatile', api_key),
        debug=DebugConfig(save_html=False),
    )
    pipeline = Pipeline(config, contract=MyContract)

#### `validate_api_key_env`

`validate_api_key_env() -> YosoiConfig`

Resolve API key for the selected provider, falling back to others if needed.

Resolution order:
1. Use api_key if already set on the LLMConfig.
2. Try the environment variable for the selected provider.
3. Walk PROVIDER_FALLBACK_ORDER and use the first provider with a key.
4. Raise if nothing works.

## Functions

### `auto_config`

`auto_config(model: str | None = None, debug: bool = False) -> YosoiConfig`

Auto-detect LLM provider and build config.

Resolution order:
1. Explicit ``model`` argument (``provider:model-name`` format)
2. ``$YOSOI_MODEL`` environment variable
3. First provider with an available API key
4. Groq default fallback
**Args:**

- `model` `str | None` — Model string in ``provider:model-name`` format, or None.
- `debug` `bool` — Whether to enable debug HTML saving.

**Returns:** `YosoiConfig` — Validated YosoiConfig.

**Raises:**

- `ValueError` — On configuration errors (bad model format, no API key, etc.).

### `css`

`css(value: str) -> SelectorEntry`

Create a CSS SelectorEntry.

### `discover`

`discover() -> SelectorEntry`

Sentinel: AI will discover the root for this scoped nested contract.

### `jsonld`

`jsonld(value: str) -> SelectorEntry`

Create a JSON-LD SelectorEntry.

### `load_urls_from_file`

`load_urls_from_file(filepath: str) -> list[str]`

Load URLs from a file (JSON, plain text, CSV, Excel, Parquet, or Markdown).
**Args:**

- `filepath` `str` — Path to file containing URLs.

**Returns:** `list[str]` — List of URL strings.

**Raises:**

- `FileNotFoundError` — If file does not exist.
- `ValueError` — If file format requires unavailable dependencies.

### `regex`

`regex(value: str) -> SelectorEntry`

Create a regex SelectorEntry.

### `register_coercion`

`register_coercion(type_name: str, description: str = '', config_defaults: Any = {}) -> Callable[[Callable[..., CoercedValue]], Callable[..., Any]]`

Decorator that registers a coercion function and returns a Field factory.

The decorated function becomes the Field factory — its name is what you use
in a Contract.  The coercion logic is stored internally in the registry.

Decorator kwargs define the config schema:
- ``description``: default field description
- all other kwargs: config keys that appear in ``json_schema_extra`` and are
  forwarded to the coerce function via ``config``
**Args:**

- `type_name` `str` — The ``yosoi_type`` identifier (e.g. ``'price'``).
- `description` `str` — Default field description shown in manifests and to the AI.
- `**config_defaults` `Any` — Config keys with their default values. These become
keyword arguments on the generated factory function.

Example::

    @register_coercion('phone', description='A phone number', country_code='+1')
    def PhoneNumber(v, config, source_url=None):
        import re
        digits = re.sub(r'\D', '', str(v))
        return config.get('country_code', '+1') + digits

    # PhoneNumber is now a Field factory:
    # PhoneNumber(country_code='+44') -> Field(json_schema_extra={...})

### `resolve_contract`

`resolve_contract(name: str) -> type[Contract]`

Resolve a contract name to a Contract class (exact matching only).

This is the programmatic API. No fuzzy matching or file scanning is
performed — those are CLI-only DX features in ``SchemaParamType``.

Resolution order:
1. Exact match in BUILTIN_SCHEMAS
2. Case-insensitive match in BUILTIN_SCHEMAS
3. Exact / case-insensitive match in _CONTRACT_REGISTRY (custom schemas)
4. Dynamic import via ``path:ClassName``
**Args:**

- `name` `str` — Contract name or ``path:ClassName`` string.

**Returns:** `type[Contract]` — The resolved Contract subclass.

**Raises:**

- `ValueError` — If no matching contract is found.

### `xpath`

`xpath(value: str) -> SelectorEntry`

Create an XPath SelectorEntry.

## Type Factories

### `Author`

`Author(description: str = ..., kwargs: Any = {}) -> Any`

### `BodyText`

`BodyText(description: str = ..., kwargs: Any = {}) -> Any`

### `Datetime`

`Datetime(description: str = ..., assume_utc: bool = ..., past_only: bool = ..., as_iso: bool = ..., kwargs: Any = {}) -> Any`

### `Field`

`Field(hint: str | None = None, frozen: bool = False, selector: str | None = None, delimiter: str | None = None, kwargs: Any = {}) -> Any`

Yosoi-aware Field wrapper that stores hints in json_schema_extra.
**Args:**

- `hint` `str | None` — Optional scraping hint that guides the AI selector discovery.
- `frozen` `bool` — If True, marks the field as frozen (selector won't be re-discovered).
- `selector` `str | None` — Optional CSS selector override. When set, AI discovery is skipped
for this field and the provided selector is used directly.
- `delimiter` `str | None` — Optional regex pattern for splitting delimited strings in list fields.
Defaults to comma/semicolon/and splitting when not set.
- `**kwargs` `Any` — Additional arguments forwarded to pydantic.Field.

**Returns:** `Any` — A pydantic FieldInfo with Yosoi-specific metadata in json_schema_extra.

### `Price`

`Price(description: str = ..., currency_symbol: str | None = ..., require_decimals: bool = ..., kwargs: Any = {}) -> Any`

### `Rating`

`Rating(description: str = ..., as_float: bool = ..., scale: int = ..., kwargs: Any = {}) -> Any`

### `Title`

`Title(description: str = ..., kwargs: Any = {}) -> Any`

### `Url`

`Url(description: str = ..., require_https: bool = ..., strip_tracking: bool = ..., kwargs: Any = {}) -> Any`

### `YosoiType`

`YosoiType(...)`

Optional base class for user-defined Yosoi semantic types.

The preferred pattern is the ``@register_coercion`` decorator — it handles
both registration and Field factory generation in one step::

    @register_coercion('phone', description='A phone number', country_code='+1')
    def PhoneNumber(v, config, source_url=None):
        import re
        digits = re.sub(r'\D', '', str(v))
        return config.get('country_code', '+1') + digits

    # PhoneNumber is now a Field factory:
    # PhoneNumber(country_code='+44') -> Field(json_schema_extra={...})

Subclassing ``YosoiType`` is useful when you prefer the OOP style and want
to group the factory and coercer under one class name::

    class PhoneNumber(YosoiType):
        type_name = 'phone'

        @staticmethod
        def coerce(v, config, source_url=None):
            import re
            digits = re.sub(r'\D', '', str(v))
            return config.get('country_code', '+1') + digits

        @classmethod
        def field(cls, country_code='+1', description='A phone number', **kwargs):
            from yosoi.types.field import Field
            return Field(
                description=description,
                json_schema_extra={'yosoi_type': cls.type_name, 'country_code': country_code},
                **kwargs,
            )

## Provider Helpers

### `alibaba`

`alibaba(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Alibaba Cloud DashScope.
**Args:**

- `model_name` `str` — DashScope model identifier (e.g. 'qwen-plus', 'qwen-max')
- `api_key` `str | None` — DashScope API key. If omitted, reads from DASHSCOPE_API_KEY or ALIBABA_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Alibaba DashScope.

### `anthropic`

`anthropic(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Anthropic (Claude).
**Args:**

- `model_name` `str` — Model identifier (e.g. 'claude-opus-4-5', 'claude-sonnet-4-6')
- `api_key` `str | None` — Anthropic API key. If omitted, reads from ANTHROPIC_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Anthropic.

### `azure`

`azure(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Azure OpenAI.

Supply ``azure_endpoint`` and optionally ``api_version`` via ``extra_params``.
**Args:**

- `model_name` `str` — Azure deployment name (e.g. 'gpt-4o')
- `api_key` `str | None` — Azure OpenAI API key. If omitted, reads from AZURE_OPENAI_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Azure OpenAI.

### `bedrock`

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

### `cerebras`

`cerebras(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Cerebras.
**Args:**

- `model_name` `str` — Cerebras model identifier (e.g. 'llama-3.3-70b')
- `api_key` `str | None` — Cerebras API key. If omitted, reads from CEREBRAS_API_KEY or CEREBRAS_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Cerebras.

### `deepseek`

`deepseek(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for DeepSeek.
**Args:**

- `model_name` `str` — DeepSeek model identifier (e.g. 'deepseek-chat', 'deepseek-reasoner')
- `api_key` `str | None` — DeepSeek API key. If omitted, reads from DEEPSEEK_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for DeepSeek.

### `fireworks`

`fireworks(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Fireworks AI.
**Args:**

- `model_name` `str` — Fireworks model identifier (e.g. 'accounts/fireworks/models/llama-v3p3-70b-instruct')
- `api_key` `str | None` — Fireworks API key. If omitted, reads from FIREWORKS_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Fireworks.

### `gemini`

`gemini(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Gemini (Google).
**Args:**

- `model_name` `str` — Gemini model identifier (e.g. 'gemini-2.0-flash')
- `api_key` `str | None` — Google API key. If omitted, reads from GEMINI_API_KEY, GEMINI_KEY, or GOOGLE_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Gemini.

### `github`

`github(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for GitHub Models.
**Args:**

- `model_name` `str` — GitHub Models identifier (e.g. 'gpt-4o', 'Llama-3.3-70B-Instruct')
- `api_key` `str | None` — GitHub token. If omitted, reads from GITHUB_TOKEN.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for GitHub Models.

### `grok`

`grok(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Grok via xAI's OpenAI-compatible endpoint.
**Args:**

- `model_name` `str` — Grok model identifier (e.g. 'grok-3', 'grok-3-mini')
- `api_key` `str | None` — xAI API key. If omitted, reads from XAI_API_KEY or GROK_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Grok.

### `groq`

`groq(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Groq.
**Args:**

- `model_name` `str` — Groq model identifier (e.g. 'llama-3.3-70b-versatile')
- `api_key` `str | None` — Groq API key. If omitted, reads from GROQ_API_KEY or GROQ_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Groq.

### `heroku`

`heroku(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Heroku Managed Inference.
**Args:**

- `model_name` `str` — Heroku model identifier (e.g. 'claude-3-5-sonnet')
- `api_key` `str | None` — Heroku inference key. If omitted, reads from HEROKU_INFERENCE_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Heroku.

### `huggingface`

`huggingface(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for HuggingFace Inference API.
**Args:**

- `model_name` `str` — HuggingFace model ID (e.g. 'Qwen/Qwen3-235B-A22B')
- `api_key` `str | None` — HF token. If omitted, reads from HF_TOKEN or HUGGINGFACE_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields (e.g. extra_params={'provider_name': 'nebius'}).

**Returns:** `LLMConfig` — Configured LLMConfig for HuggingFace.

### `litellm`

`litellm(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for LiteLLM proxy.

Supply ``api_base`` via ``extra_params`` to point at your LiteLLM proxy
endpoint.
**Args:**

- `model_name` `str` — Model identifier passed through to LiteLLM
- `api_key` `str | None` — API key for the proxied provider. If omitted, reads from LITELLM_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for LiteLLM.

### `mistral`

`mistral(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Mistral.
**Args:**

- `model_name` `str` — Mistral model identifier (e.g. 'mistral-large-latest')
- `api_key` `str | None` — Mistral API key. If omitted, reads from MISTRAL_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Mistral.

### `moonshotai`

`moonshotai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for MoonshotAI (Kimi).
**Args:**

- `model_name` `str` — Moonshot model identifier (e.g. 'kimi-k2-0711-preview')
- `api_key` `str | None` — Moonshot API key. If omitted, reads from MOONSHOT_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for MoonshotAI.

### `nebius`

`nebius(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Nebius AI Studio.
**Args:**

- `model_name` `str` — Nebius model identifier (e.g. 'Qwen/Qwen3-235B-A22B-fast')
- `api_key` `str | None` — Nebius API key. If omitted, reads from NEBIUS_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Nebius.

### `ollama`

`ollama(model_name: str, kwargs: Any = {}) -> LLMConfig`

Quick config for Ollama (local).

No API key required. Supply ``base_url`` via ``extra_params`` to override
the default ``http://localhost:11434``.
**Args:**

- `model_name` `str` — Ollama model tag (e.g. 'llama3', 'mistral', 'qwen2.5')
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Ollama.

### `openai`

`openai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OpenAI.
**Args:**

- `model_name` `str` — OpenAI model identifier (e.g. 'gpt-4o', 'gpt-4o-mini')
- `api_key` `str | None` — OpenAI API key. If omitted, reads from OPENAI_API_KEY or OPENAI_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OpenAI.

### `openrouter`

`openrouter(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OpenRouter.
**Args:**

- `model_name` `str` — OpenRouter model identifier (e.g. 'meta-llama/llama-3.3-70b-instruct:free')
- `api_key` `str | None` — OpenRouter API key. If omitted, reads from OPENROUTER_API_KEY or OPENROUTER_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OpenRouter.

### `ovhcloud`

`ovhcloud(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for OVHcloud AI Endpoints.
**Args:**

- `model_name` `str` — OVHcloud model identifier
- `api_key` `str | None` — OVH access token. If omitted, reads from OVH_AI_ENDPOINTS_ACCESS_TOKEN.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for OVHcloud.

### `provider`

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

### `sambanova`

`sambanova(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for SambaNova.
**Args:**

- `model_name` `str` — SambaNova model identifier (e.g. 'Meta-Llama-3.3-70B-Instruct')
- `api_key` `str | None` — SambaNova API key. If omitted, reads from SAMBANOVA_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for SambaNova.

### `together`

`together(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Together AI.
**Args:**

- `model_name` `str` — Together model identifier (e.g. 'meta-llama/Llama-3-70b-chat-hf')
- `api_key` `str | None` — Together API key. If omitted, reads from TOGETHER_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Together AI.

### `vercel`

`vercel(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for Vercel AI.
**Args:**

- `model_name` `str` — Vercel AI model identifier
- `api_key` `str | None` — Vercel API key. If omitted, reads from AI_SDK_KEY or VERCEL_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for Vercel AI.

### `vertexai`

`vertexai(model_name: str, kwargs: Any = {}) -> LLMConfig`

Quick config for Google Vertex AI.

No API key required — uses GCP application default credentials or a
service account file supplied via ``extra_params``.
**Args:**

- `model_name` `str` — Vertex AI model ID (e.g. 'gemini-2.0-flash-001')
- `**kwargs` `Any` — Additional LLMConfig fields (e.g. extra_params={'project_id': '...', 'region': 'us-east1'}).

**Returns:** `LLMConfig` — Configured LLMConfig for Google Vertex AI.

### `xai`

`xai(model_name: str, api_key: str | None = None, kwargs: Any = {}) -> LLMConfig`

Quick config for xAI (Grok models via native xAI client).
**Args:**

- `model_name` `str` — xAI model identifier (e.g. 'grok-3', 'grok-3-mini')
- `api_key` `str | None` — xAI API key. If omitted, reads from XAI_API_KEY.
- `**kwargs` `Any` — Additional LLMConfig fields.

**Returns:** `LLMConfig` — Configured LLMConfig for xAI.
