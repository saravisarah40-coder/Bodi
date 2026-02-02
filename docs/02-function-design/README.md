# Function Design

## Overview

Functions are the smallest unit of behavior in backend systems. Clean function
design keeps business logic predictable, testable, and safe to change.

## Core Principles

- Do one thing.
- Keep functions small and easy to scan.
- Make side effects explicit.
- Use clear and consistent input/output shapes.
- Prefer pure functions for business rules.

## Size and Complexity

- Aim for short functions (often under 30 lines).
- Keep nesting shallow; use guard clauses.
- Extract helper functions when the name improves clarity.

**Bad**
```python
def create_order(data):
    if data and data.get("items"):
        total = 0
        for item in data["items"]:
            if item["qty"] > 0:
                total += item["price"] * item["qty"]
        if total > 0:
            return Order(total=total)
```

**Good**
```python
def create_order(payload: OrderPayload) -> Order:
    validate_order_payload(payload)
    total = calculate_order_total(payload.items)
    return Order(total=total)
```

## Arguments

- Prefer 0-2 parameters; use objects for larger inputs.
- Use keyword-only arguments for clarity.
- Avoid boolean flags that change behavior.

```python
def send_email(*, recipient: str, subject: str, body: str) -> None:
    ...
```

## Return Values

- Return a single, predictable type.
- Use `Optional[T]` when `None` is valid and expected.
- Prefer domain objects over tuple returns.

```python
def get_user(user_id: str) -> Optional[User]:
    ...
```

## Side Effects

- Separate I/O from business logic.
- Keep state mutation localized.
- Do not modify inputs in-place unless documented.

```python
def calculate_discount(items: list[Item]) -> Decimal:
    return sum(item.discount for item in items)
```

## Async and I/O

- Use `async` for I/O-bound operations.
- Avoid blocking calls inside async functions.
- Offload CPU-bound work with `asyncio.to_thread`.

```python
async def fetch_profile(client: httpx.AsyncClient, user_id: str) -> Profile:
    response = await client.get(f"/users/{user_id}")
    response.raise_for_status()
    return Profile.model_validate(response.json())
```

## Error Handling

- Fail fast on invalid inputs.
- Raise domain-specific exceptions for business rules.
- Let frameworks translate exceptions to HTTP responses.
