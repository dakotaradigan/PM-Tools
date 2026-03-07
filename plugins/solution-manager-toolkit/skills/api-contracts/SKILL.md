---
name: api-contracts
description: This skill should be used when defining contract-first API specifications with schemas, error handling, versioning, and consumer alignment for solution management.
---

# API Contracts

Domain knowledge for contract-first API specification.

## When to Use

- User asks to define an API, endpoint, or service contract
- Building OpenAPI/Swagger specs or GraphQL schemas
- Reviewing API designs for completeness

## Contract Components

For each endpoint: method, path, request/response schemas, error codes, auth requirements, rate limits, versioning, pagination, idempotency, and examples.

## Key Principles

- Contract-first: define the spec before writing code.
- Validate against the API checklist in `references/domain-knowledge-base.md`.
- Error responses are as important as success responses — document every error code.
- Consumers should review contracts before implementation begins.
- Backward compatibility rules must be explicit from day one.
- Include domain-specific headers or fields from `references/domain-knowledge.md`.
