# Documentation

## Overview

Documentation keeps a backend maintainable as teams and systems grow. It should
be accurate, concise, and close to the code.

## Core Principles

- Keep docs near the implementation.
- Prefer examples over long prose.
- Update docs as part of code changes.

## Docstrings

- Use clear docstrings for public functions and classes.
- Document inputs, outputs, and raised exceptions.

```python
def calculate_tax(amount: Decimal) -> Decimal:
    """Return tax amount for a given price."""
    ...
```

## API Documentation

- FastAPI generates OpenAPI automatically.
- For Django, consider DRF + schema generation tools.
- Document error responses and rate limits.

## README and Runbooks

- Include setup steps, env variables, and local run commands.
- Add runbooks for common operational issues.

## Architecture Decision Records (ADRs)

- Record major decisions and trade-offs.
- Keep ADRs short and dated.

## Code Comments

- Comment "why", not "what".
- Avoid redundant comments.
