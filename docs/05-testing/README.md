# Testing

## Overview

Backend systems require a balanced testing strategy that catches regressions
without slowing delivery. Use the testing pyramid as a guide.

## Core Principles

- Keep most tests at the unit level.
- Cover critical flows with integration and API tests.
- Tests should be deterministic and fast.
- Test behavior, not implementation details.

## Testing Pyramid

1. **Unit tests**: pure business logic.
2. **Integration tests**: databases, queues, external APIs.
3. **End-to-end/API tests**: full request flow.

## Unit Tests

- Use `pytest` for concise tests.
- Isolate logic with pure functions.
- Avoid hitting external services.

```python
def test_calculate_total():
    assert calculate_total([Item(price=10, qty=2)]) == 20
```

## Integration Tests

- Use a test database.
- Roll back state between tests.
- Validate repository and service behavior.

## API Tests (FastAPI)

```python
from fastapi.testclient import TestClient

def test_create_user(client: TestClient):
    response = client.post("/users", json={"email": "a@b.com"})
    assert response.status_code == 201
```

## API Tests (Django)

```python
def test_create_user(client):
    response = client.post("/users/", data={"email": "a@b.com"})
    assert response.status_code == 201
```

## Fixtures and Mocking

- Use fixtures for shared setup.
- Mock external services, not your own code.
- Keep mocks aligned with real interfaces.

## Coverage and CI

- Track coverage for core domain logic.
- Fail CI on broken tests.
- Keep test runtime predictable.
