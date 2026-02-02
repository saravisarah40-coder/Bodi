# Code Organization

## Overview

Good structure keeps backend systems scalable and understandable. Organize code
by feature boundaries and keep dependencies flowing in the right direction.

## Core Principles

- Group by domain or feature, not only by type.
- Keep boundaries between layers clear.
- Avoid circular dependencies.
- Keep framework-specific code at the edges.

## Project Structure (FastAPI)

```
app/
  api/
    v1/
      routers/
  domain/
  services/
  repositories/
  schemas/
  settings.py
```

## Project Structure (Django)

```
project/
  settings/
  urls.py
apps/
  users/
  orders/
```

## Layers and Boundaries

- **Presentation**: API routes, serializers.
- **Application**: use cases, orchestration.
- **Domain**: business rules.
- **Infrastructure**: database, HTTP clients.

## Settings and Configuration

- Use environment variables for secrets.
- Separate settings for dev/staging/prod.
- Validate settings at startup.

## Dependency Management

- Pin versions in `requirements.txt` or use Poetry.
- Separate dev and prod dependencies.
- Review dependency updates regularly.

## Migrations and Schema Changes

- Keep migrations small and reviewable.
- Add indexes for query-heavy fields.
- Avoid destructive migrations without a plan.

## Background Jobs and API Versioning

- Offload long tasks to Celery or RQ.
- Make jobs idempotent and retry-safe.
- Version APIs by path (`/v1/`) or headers.
