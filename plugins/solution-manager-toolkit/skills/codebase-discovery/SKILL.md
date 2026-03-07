---
name: codebase-discovery
description: This skill should be used when comprehending an existing codebase to extract data models, API endpoints, dependencies, and architectural patterns for solution management context.
---

# Codebase Discovery

Domain knowledge for analyzing existing codebases to build solution context.

## When to Use

- User asks to "discover", "map", or "analyze" an existing codebase
- Starting a new project that builds on existing systems
- Need to understand what data models, APIs, or integrations already exist

## Discovery Targets

1. **Data models** — ORM classes, database schemas, entity definitions
2. **API endpoints** — REST routes, GraphQL schemas, gRPC service definitions
3. **Dependencies** — External services, vendor integrations, shared libraries
4. **Configuration** — Environment variables, feature flags, deployment topology
5. **Event producers/consumers** — Message queues, pub/sub, webhooks

## Key Principles

- Read code, don't assume. Discovery is observation, not inference.
- Map relationships between entities, not just individual definitions.
- Flag undocumented dependencies — they are the highest-risk items.
- Capture the current state, not the intended state.
