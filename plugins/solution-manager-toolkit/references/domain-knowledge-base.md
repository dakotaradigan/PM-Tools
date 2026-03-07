# Domain Knowledge Base

Generic structural checklists and templates for solution management. This file provides the structural scaffolding that domain knowledge builds on.

> **For teams customizing this toolkit:**
> - This file contains generic checklists that apply broadly. You should NOT need to modify it.
> - If your team has additional checklist items beyond what's here, ADD them to the relevant section — don't remove existing items.
> - Domain-specific content goes in `domain-knowledge.md`.
> - Team-specific systems, custodians, and org details go in `team-context.md`.

## Data Model Completeness Checklist

For each data entity in a canonical data model:
- [ ] Entity name and description defined
- [ ] All attributes listed with data types
- [ ] Primary key / unique identifier specified
- [ ] Relationships to other entities documented (FK, association type)
- [ ] Required vs optional attributes marked
- [ ] Default values specified where applicable
- [ ] Enumerated value sets defined for constrained fields
- [ ] Versioning / history tracking strategy documented
- [ ] Data ownership (steward, source system) assigned
- [ ] Validation rules / constraints documented
- [ ] Example values provided for each attribute

## API Contract Completeness Checklist

For each API endpoint:
- [ ] HTTP method and path defined
- [ ] Request schema (body, query params, headers) documented
- [ ] Response schema for success cases documented
- [ ] Error response schemas and codes documented
- [ ] Authentication / authorization requirements specified
- [ ] Rate limiting / throttling policy stated
- [ ] Versioning strategy documented (URL path, header, query param)
- [ ] Pagination approach defined (cursor, offset, keyset)
- [ ] Idempotency requirements specified for mutating operations
- [ ] Content negotiation (Accept headers) documented
- [ ] Deprecation policy stated
- [ ] Example request/response pairs provided

## Event Specification Completeness Checklist

For each event in the system:
- [ ] Event name and description defined
- [ ] Event schema (payload structure) documented
- [ ] Producer(s) identified
- [ ] Consumer(s) identified
- [ ] Trigger conditions specified
- [ ] Delivery guarantee stated (at-most-once, at-least-once, exactly-once)
- [ ] Ordering guarantee stated (ordered, unordered, per-key)
- [ ] Retry / dead-letter policy documented
- [ ] Schema evolution strategy defined (backward, forward, full compatibility)
- [ ] Event versioning approach documented
- [ ] Idempotency key specified
- [ ] Expected volume / throughput documented

## NFR Format Template

Every non-functional requirement should follow this structure:

```
Quality: [The quality attribute — e.g., Latency, Availability, Throughput]
Target: [Measurable target — e.g., p99 < 200ms]
Conditions: [Under what conditions — e.g., peak load, 10k concurrent users]
Measurement: [How it will be verified — e.g., APM dashboard, load test, audit log query]
Priority: [Must Have | Should Have | Could Have]
Source: [Where this requirement came from — research, regulation, SLA]
```

## Requirements Review Patterns

When reviewing requirements for completeness:

### Traceability
- Every requirement traces to a source (research finding, regulation, business rule)
- No orphan requirements (requirements with no source)
- No orphan findings (research findings with no corresponding requirement)

### Testability
- Every requirement has measurable acceptance criteria
- Acceptance criteria use Given/When/Then format
- Edge cases and error conditions are specified

### Consistency
- No contradictions between requirements
- Shared terminology used consistently across all artifacts
- Data entity names match between data model, API contracts, and event specs

### Completeness
- CRUD coverage: can each entity be Created, Read, Updated, Deleted (or explicitly excluded)?
- Lifecycle coverage: are all state transitions defined?
- Error coverage: what happens when things fail?
- Security: access control defined for each operation?

## Architecture Tradeoff Framework

For each significant architecture decision:

| Dimension | Option A | Option B | Option C |
|-----------|----------|----------|----------|
| **Approach** | | | |
| **Pros** | | | |
| **Cons** | | | |
| **Latency impact** | | | |
| **Complexity** | | | |
| **Operational cost** | | | |
| **Team familiarity** | | | |
| **Reversibility** | | | |
| **Risk** | | | |

Decision criteria (rank by priority for this context):
1. [Most important quality attribute]
2. [Second most important]
3. [Third most important]

## Solution State Template Structure

The `solution_state.md` file tracks cumulative progress:

```yaml
project: [Project name]
status: [discovery | definition | design | delivery]
last_updated: [ISO date]

artifacts:
  research_synthesis: [not started | in progress | complete]
  data_model: [not started | in progress | complete]
  api_contracts: [not started | in progress | complete]
  event_specs: [not started | in progress | complete]
  nfrs: [not started | in progress | complete]
  architecture: [not started | in progress | complete]

open_questions: []
decisions: []
risks: []
```
