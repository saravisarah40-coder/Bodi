# Security

## Overview

Security is a cross-cutting concern in backend systems. The goal is to reduce
attack surface, protect data, and ensure predictable behavior under attack.

## Core Principles

- Validate all input.
- Apply least privilege.
- Keep secrets out of code and logs.
- Patch dependencies regularly.

## Input Validation

- Validate at the API boundary with Pydantic or Django serializers.
- Enforce max sizes for payloads, files, and query parameters.

## Authentication and Authorization

- Use proven auth mechanisms (JWT, sessions, OAuth).
- Hash passwords with bcrypt or argon2.
- Enforce object-level permissions.

## Secrets and Configuration

- Store secrets in environment variables or secret managers.
- Rotate keys and tokens.
- Never log credentials or tokens.

## Dependency Security

- Pin versions and review updates.
- Use tools like `pip-audit` or `safety`.
- Remove unused dependencies.

## Headers, CORS, and CSRF

- Set secure headers (HSTS, X-Content-Type-Options).
- Configure CORS explicitly.
- Use CSRF protection for cookie-based sessions.

## Rate Limiting and Abuse Protection

- Apply per-IP or per-user limits.
- Protect login and password reset endpoints.

## Data Protection

- Encrypt data in transit (TLS).
- Encrypt sensitive data at rest.
- Apply data retention policies.
