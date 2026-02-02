# Error Handling

## Overview

Robust error handling prevents silent failures and protects users from
unexpected behavior. Backend systems must translate internal errors into safe,
consistent responses.

## Key Principles

- Fail fast on invalid input.
- Use specific exception types.
- Log errors with context, not secrets.
- Return consistent error responses.
- Prefer recovery strategies over retries everywhere.

## Error Types and Classification

- **Validation errors**: bad input, missing fields, invalid formats.
- **Domain errors**: business rule violations.
- **Infrastructure errors**: database, network, or third-party failures.

```python
class DomainError(Exception):
    pass

class PaymentDeclinedError(DomainError):
    pass
```

## Try/Except Patterns

- Keep `try` blocks small.
- Catch specific exceptions.
- Re-raise or wrap with context.

```python
try:
    charge_id = gateway.charge(amount)
except GatewayTimeoutError as exc:
    raise PaymentServiceUnavailableError() from exc
```

## Async Error Handling

- Exceptions propagate across `await`.
- Use `asyncio.gather(..., return_exceptions=True)` carefully.
- Add explicit timeouts for I/O.

```python
async with asyncio.timeout(2):
    data = await client.get("/health")
```

## HTTP Error Responses (FastAPI/Django)

- Map domain errors to HTTP statuses.
- Avoid leaking stack traces or internal details.

**FastAPI**
```python
raise HTTPException(status_code=409, detail="Order already finalized")
```

**Django**
```python
from django.core.exceptions import PermissionDenied
raise PermissionDenied("Access denied")
```

## Logging and Monitoring

- Include request IDs and user context.
- Avoid logging secrets or PII.
- Use structured logging where possible.

```python
logger.exception("payment_failed", extra={"order_id": order.id})
```

## Recovery and Retries

- Retry only transient errors.
- Use exponential backoff with a max retry limit.
- Prefer circuit breakers for unstable dependencies.

## Testing Error Scenarios

- Unit test domain exceptions.
- API test error response schema.
- Include timeout and retry tests for integrations.
