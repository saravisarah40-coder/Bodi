# Architecture

## Overview

Architecture defines how components interact, where dependencies flow, and how
teams can evolve a system safely. For Python backends, prioritize modularity and
clear boundaries.

## Core Principles

- Separate concerns by layer and domain.
- Keep dependencies pointing inward.
- Make contracts explicit.
- Optimize for change, not just current needs.

## Clean Architecture (Pragmatic)

- **Entities**: core business rules.
- **Use cases**: application logic.
- **Adapters**: database, HTTP, queues.
- **Frameworks**: FastAPI/Django at the edges.

## Hexagonal (Ports and Adapters)

- Define ports for external interactions.
- Implement adapters for databases and APIs.
- Swap adapters without changing domain logic.

## DDD-Lite

- Identify bounded contexts.
- Keep aggregates consistent.
- Use ubiquitous language in code.

## Event-Driven Patterns

- Use domain events for decoupling.
- Ensure idempotency and ordering.
- Consider the outbox pattern for reliability.

## Service Boundaries

- Start with a modular monolith.
- Split services only when teams or scale demand it.
- Avoid distributed monoliths with tight coupling.

## Deployment Architecture

- Separate web, worker, and scheduler processes.
- Add a cache layer when needed.
- Keep configuration and secrets external.
