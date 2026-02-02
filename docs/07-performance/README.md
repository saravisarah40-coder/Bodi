# Performance

## Overview

Performance is about delivering consistent latency and throughput without
over-optimizing. Focus on measurement and the largest bottlenecks.

## Core Principles

- Measure before optimizing.
- Optimize the slowest paths first.
- Avoid premature caching.
- Keep database queries efficient.

## Profiling and Observability

- Use `cProfile`, `pyinstrument`, or APM tools.
- Monitor p95/p99 latency, error rates, and throughput.

## Database Performance

- Add indexes for common filters and joins.
- Avoid N+1 queries; use eager loading.
- Batch writes when possible.

## Caching

- Cache hot read paths with Redis or in-memory stores.
- Use clear cache keys and invalidation rules.
- Avoid caching user-specific data without segmentation.

## Async and Concurrency

- Use async for I/O-bound endpoints.
- Avoid blocking operations in async code.
- Configure workers (gunicorn/uvicorn) based on CPU cores.

## Serialization and Validation

- Limit response payload size.
- Avoid heavy validation in tight loops.
- Use fast JSON libraries when needed (for example, orjson).

## Common Bottlenecks

- Large ORM queries without pagination.
- Excessive logging in hot paths.
- Unbounded concurrency or retries.
