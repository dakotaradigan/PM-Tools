---
name: event-integration
description: This skill should be used when defining event schemas, delivery guarantees, and integration patterns for asynchronous communication in solution architectures.
---

# Event Integration

Domain knowledge for event-driven integration specifications.

## When to Use

- User asks to define events, messages, or async integrations
- Designing pub/sub, event sourcing, or message queue architectures
- Reviewing event schemas for completeness

## Event Components

For each event: name, schema, producer, consumer, trigger, delivery guarantee, ordering, retry policy, schema evolution strategy, versioning, idempotency key, and throughput.

## Key Principles

- Every event needs a defined delivery guarantee — don't default to "best effort."
- Validate against the event checklist in `references/domain-knowledge-base.md`.
- Schema evolution strategy prevents breaking consumers on change.
- Idempotency keys are mandatory for at-least-once delivery.
- Dead-letter queues need monitoring and reprocessing procedures.
- Check `references/domain-knowledge.md` for domain-specific event patterns.
