---
title: Validators
description: Transform and normalise extracted values without boilerplate.
---

Yosoi offers two layers of field-level validation: built-in type coercions that handle the common cases, and a `Validators` inner class for custom transforms.

## Built-in coercions

Field types like `ys.Price()`, `ys.Title()`, and `ys.Author()` coerce raw strings automatically -- no `@field_validator` needed.

```python
import yosoi as ys

class Product(ys.Contract):
    title: str = ys.Title()
    price: float = ys.Price(hint='Book price, always includes £ symbol')
    rating: str = ys.Rating(hint="Star rating written as a word e.g. 'Three'")
```

```python
raw = {'title': '  A Light in the Attic  ', 'price': '£12.99', 'rating': '  Three  '}
result = Product.model_validate(raw)

# result.title  == 'A Light in the Attic'   (whitespace stripped)
# result.price  == 12.99                     (float, £ stripped)
# result.rating == 'Three'                   (whitespace stripped)
```

## Validators inner class

For custom per-field transforms, define static methods inside a `Validators` class. They run before Pydantic's [△](#ref-1) own validation. No decorator ceremony required.

```python
class BookStore(ys.Contract):
    title: str = ys.Title()
    price: float = ys.Price(hint='Book price including currency symbol')
    category: str = ys.Field(hint='Genre or category label')

    class Validators:
        @staticmethod
        def title(v: str) -> str:
            """Truncate very long titles to 60 characters."""
            return v[:60].rstrip() + ('...' if len(v) > 60 else '')

        @staticmethod
        def category(v: str) -> str:
            """Normalise category to title case."""
            return v.strip().title()
```

```python
raw = {
    'title': 'The Very Long Title That Goes On and On and Eventually Exceeds Sixty Characters',
    'price': '$1,234.56',
    'category': '  science fiction  ',
}
result = BookStore.model_validate(raw)

# result.title    == 'The Very Long Title That Goes On and On and Eventually...'
# result.price    == 1234.56   ($ and , stripped by ys.Price)
# result.category == 'Science Fiction'
```

Each method name must match the field name it transforms. Methods that don't match any field are silently ignored.

## FAQs

<details>
<summary>Can I raise an error inside a Validators method?</summary>

Yes. Raise a standard `ValueError` and Pydantic will wrap it into a `ValidationError` as usual.

</details>

<details>
<summary>Do validators run on list[T] fields element-by-element?</summary>

No. The validator receives the full list as its argument. If you need per-element processing, iterate inside the method.

</details>

<details>
<summary>Can I use async validators?</summary>

No. `Validators` methods must be synchronous static methods. For async post-processing, handle it after `model_validate()` returns.

</details>

<details>
<summary>What is the execution order?</summary>

`Validators` methods run first, then built-in type coercions, then Pydantic's own validation. This means your custom transforms see the raw extracted string before any coercion has been applied.

</details>

## References

<a id="ref-1"></a>△ **Pydantic**. Pydantic Services Inc. *Data validation library for Python.* https://docs.pydantic.dev/
