# Class Design

## Overview

Classes organize state and behavior. In backend systems, clean class design
keeps domain logic isolated, makes dependencies explicit, and simplifies tests.

## Core Principles

- Single Responsibility: one reason to change.
- Prefer composition over inheritance.
- Make dependencies explicit.
- Keep data models simple and validated.

## Responsibilities

- Services should orchestrate, not do everything.
- Repositories should only handle persistence.
- Avoid "God" classes with many unrelated methods.

```python
class OrderService:
    def __init__(self, repository: OrderRepository) -> None:
        self._repository = repository

    def place_order(self, payload: OrderPayload) -> Order:
        ...
```

## Composition vs Inheritance

- Favor small composable helpers.
- Use inheritance for true "is-a" relationships.
- Avoid deep class hierarchies in service layers.

## Data Classes and Pydantic Models

- Use `dataclass` for simple, trusted data containers.
- Use Pydantic models for validation at boundaries (API, persistence).

```python
@dataclass(frozen=True)
class Money:
    amount: Decimal
    currency: str
```

## Interfaces and Protocols

- Use `typing.Protocol` for testable, interface-driven design.
- Use `abc.ABC` when shared behavior is required.

```python
class PaymentProvider(Protocol):
    def charge(self, amount: Decimal) -> str:
        ...
```

## Dependency Injection

- FastAPI: prefer `Depends` for framework-managed injection.
- Django: inject services explicitly in views or commands.
- Avoid global singletons for core services.
