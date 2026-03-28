---
title: Contributing
description: How to contribute to Yosoi and who maintains the project.
---

Contributions are welcome. Below is what you need to get started.

## Setting Up

Install with dev dependencies and set up the pre-commit hooks:

```bash
uv sync --group dev

uv run pre-commit install

uv run pre-commit run --all-files
```

## Tools

| Tool | Purpose | Command |
|------|---------|---------|
| **Ruff** | Linting & Formatting | `uv run ruff check .` |
| **Mypy** | Type Checking | `uv run mypy .` |
| **Pre-commit** | Git Hooks | `uv run pre-commit run --all-files` |

## Commit Guidelines

Use [conventional commits](https://www.conventionalcommits.org/):

```bash
git commit -m "feat: add new selector discovery feature"
git commit -m "fix: handle missing author tags"
git commit -m "docs: update README with examples"
```

**Commit types:** `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

## Pull Request Guidelines

When opening a PR, please include:

1. **Intent** -- what the PR does and why.
2. **Changes** -- a summary of what was changed.
3. **GenAI usage** -- if you used AI to write any of the code, include the prompts you used.
4. **Risks** -- any risks or side effects this PR might introduce.
5. **Docs** -- if needed, there should be a related PR to the [docs repository ](https://github.com/CascadingLabs/Yosoi-Docs)

---

## Maintainers

| Name | Affiliation |
|------|------------|
| [Andrew Berg](https://github.com/AndrewPBerg) | College of Charleston, Cascading Labs |
| [Houston Miles](https://github.com/HoustonMiles) | College of Charleston, Cascading Labs |

## Team

| Name | Affiliation |
|------|------------|
| [Braeden Mefford](https://github.com/braeden-mefford) | College of Charleston, Cascading Labs |
| [Mia Wang](https://charleston.edu/compsci/faculty/wang-mia.php) | College of Charleston, Cascading Labs |
