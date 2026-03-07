---
name: solution-work:eventspec
description: Define event schemas with delivery guarantees, ordering, retry policies, and schema evolution strategies
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# Define Event Specifications

Create event schemas for asynchronous integrations with full delivery specifications.

## Steps

1. **Load references** — Read `references/domain-knowledge-base.md` for the event specification completeness checklist. Read `references/domain-knowledge.md` for domain-specific event patterns and failure modes.

2. **Check for existing context** — Look for `data-model/canonical-entities.md`, `discovery/codebase-report.md`, and `api-contracts/endpoints.md`. These inform what events are needed (state changes, notifications, integrations).

3. **For each event, define:**
   - Event name (past tense verb + noun, e.g., `OrderPlaced`, `PriceUpdated`)
   - Description and trigger conditions
   - Producer(s) and consumer(s)
   - Payload schema (reference data model entities)
   - Delivery guarantee (at-most-once, at-least-once, exactly-once)
   - Ordering guarantee (ordered, unordered, per-partition-key)
   - Retry policy and dead-letter handling
   - Schema evolution strategy (backward/forward/full compatibility)
   - Event versioning approach
   - Idempotency key specification
   - Expected volume and throughput

4. **Validate against checklist** — Run through every item in the event specification completeness checklist. Flag gaps.

5. **Cross-reference** — Verify event payload entities exist in the data model. Verify producers/consumers align with API contracts or discovered services.

6. **Check domain failure modes** — Review `references/domain-knowledge.md` for common failure modes and ensure events handle them (e.g., stale data, duplicate processing, timezone errors).

7. **Write outputs** — Write to `event-specs/`:
   - `event-specs/event-catalog.md` — Full event specifications
   - `event-specs/flow-diagram.md` — Producer → Event → Consumer flow documentation
   - `event-specs/schema-evolution.md` — Evolution and versioning rules

8. **Update solution state** — If `solution_state.md` exists, update the `event_specs` artifact status.

9. **Suggest next steps** — Recommend `nfr` for throughput and delivery targets, or `review` for cross-artifact consistency.

## Important

- Every event needs a delivery guarantee — "best effort" is not acceptable for production systems.
- Idempotency keys are mandatory for at-least-once delivery.
- Schema evolution strategy prevents breaking consumers when events change.
- Dead-letter queues need monitoring and reprocessing procedures — don't just define them, specify who acts on failures.
- Check domain knowledge for domain-specific event patterns and failure modes.
