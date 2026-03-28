---
title: Custom Types
description: Extend Yosoi with your own semantic field types.
---

When built-in types don't cover your domain, register a custom type. Once registered, it works exactly like a built-in: the AI sees it in the manifest, and the coercion runs automatically during extraction.

## Pattern 1: `@register_coercion` (preferred)

One function, zero boilerplate. The decorator registers the coerce logic and replaces the name with a `Field` factory.

```python
import re
from typing import Any
from yosoi.types.registry import register_coercion

@register_coercion('phone', description='A phone number', country_code='+1')
def PhoneNumber(v: object, config: dict[str, Any], source_url: str | None = None) -> str:
    """Strip formatting and prepend a country code."""
    raw = str(v).strip()
    digits = re.sub(r'\D', '', raw)
    if not digits:
        raise ValueError(f'No digits found in phone value: {v!r}')
    cc = config.get('country_code', '+1')
    cc_digits = re.sub(r'\D', '', cc)
    if digits.startswith(cc_digits):
        return f'+{digits}'
    return f'{cc}{digits}'
```

Decorator kwargs become the factory's parameter schema:

```python
# Default country code
us_phone: str = PhoneNumber()

# Override per field
uk_phone: str = PhoneNumber(country_code='+44')
```

## Pattern 2: `YosoiType` subclass

Useful when you prefer OOP or want to group the coerce logic and field factory under one name.

```python
import re
from typing import Any
import yosoi as ys

class ISBN(ys.YosoiType):
    """ISBN-10 or ISBN-13, normalised to digits-only."""

    type_name = 'isbn'

    @staticmethod
    def coerce(v: object, config: dict[str, Any], source_url: str | None = None) -> str:
        raw = re.sub(r'[\s\-]', '', str(v))
        if not raw.isdigit():
            raise ValueError(f'ISBN contains non-digit characters: {raw!r}')
        if config.get('require_isbn13') and len(raw) != 13:
            raise ValueError(f'Expected ISBN-13 (13 digits), got {len(raw)}: {raw!r}')
        return raw

    @classmethod
    def field(cls, require_isbn13: bool = False, description: str = 'An ISBN identifier', **kwargs: Any) -> Any:
        from yosoi.types.field import Field
        return Field(
            description=description,
            json_schema_extra={'yosoi_type': cls.type_name, 'require_isbn13': require_isbn13},
            **kwargs,
        )
```

```python
class BookListing(ys.Contract):
    title: str = ys.Title()
    author: str = ys.Author()
    price: float = ys.Price()
    isbn: str = ISBN.field()
    isbn13: str = ISBN.field(require_isbn13=True)
```

## Using custom types in a contract

Both patterns produce types that compose naturally with built-ins:

```python
import yosoi as ys

class ContactPage(ys.Contract):
    name: str = ys.Title()
    us_phone: str = PhoneNumber()
    uk_phone: str = PhoneNumber(country_code='+44')
    website: str = ys.Url()
```

Custom types appear in `Contract.generate_manifest()`, so the AI knows about them during selector discovery.

## FAQs

<details>
<summary>Which pattern should I use?</summary>

Use `@register_coercion` for most cases. It is less code and works well for simple coercions. Use `YosoiType` when you need multiple related configurations or want to organise the type as a standalone class.

</details>

<details>
<summary>Can custom types be used with list[T]?</summary>

Yes. Custom coercions run element-by-element on list fields, the same as built-in types.

</details>

<details>
<summary>How do I debug a coercion failure?</summary>

Raise a `ValueError` with a descriptive message inside your coerce function. Pydantic [△](#ref-1) will surface it as a `ValidationError` with field context. Run with `--debug` to inspect the raw extracted values before coercion.

</details>

<details>
<summary>Do I need to register a YosoiType subclass explicitly?</summary>

No. Subclassing `YosoiType` registers the type automatically. Just import the class before running discovery.

</details>

## References

<a id="ref-1"></a>△ **Pydantic**. Pydantic Services Inc. *Data validation library for Python.* https://docs.pydantic.dev/
