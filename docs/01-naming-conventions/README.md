# Naming Conventions

## Overview

Consistent naming makes backend code easier to read, search, and evolve. For
Python services, good names reduce the need for comments and help reviewers
understand intent quickly.

## Core Principles

- Use intention-revealing names.
- Avoid misleading abbreviations or overloaded words.
- Prefer clarity over brevity.
- Keep naming consistent across modules and layers.
- Align names with the domain language.

## Variables and Constants

### Guidelines
- Use nouns for variables: `user`, `invoice_total`, `order_items`.
- Use `is_`, `has_`, `can_` for booleans: `is_active`, `has_access`.
- Use plural names for collections: `users`, `line_items`.
- Use UPPER_SNAKE_CASE for constants.

### Examples

**Bad**
```python
d = 3  # days
u = get_user()
status = 1
```

**Good**
```python
days_until_expiry = 3
user = get_user()
ORDER_STATUS_PENDING = "pending"
```

## Functions and Methods

### Guidelines
- Use verbs that describe behavior: `create_order`, `validate_token`.
- Avoid generic names like `process` or `handle` without context.
- Use `get_` only for fast, in-memory access; use `fetch_` for I/O.

### Examples
```python
def fetch_user_profile(user_id: str) -> UserProfile:
    ...

def validate_checkout(payload: CheckoutPayload) -> None:
    ...
```

## Classes and Modules

### Guidelines
- Use nouns for classes: `UserService`, `PaymentGateway`.
- Use suffixes consistently: `Service`, `Repository`, `Schema`, `DTO`.
- Django model classes should be singular nouns: `Order`, `Invoice`.
- Pydantic models should describe role: `UserCreate`, `UserResponse`.

### Examples
```python
class UserRepository:
    ...

class OrderCreate(BaseModel):
    ...
```

## Files and Packages

### Guidelines
- Use `snake_case` for file names: `user_service.py`.
- Group by feature/domain, not by type alone.
- Avoid names that shadow stdlib modules (`email.py`, `json.py`).

### Example Structure
```
app/
  users/
    router.py
    service.py
    repository.py
    schemas.py
```

## Python-Specific Considerations

- Use `self` and `cls` consistently.
- Exception classes should end with `Error`: `PaymentError`.
- Avoid `from x import *`.
- Prefer `Path` over raw string paths when possible.
