---
name: nfr-definition
description: This skill should be used when defining non-functional requirements with measurable targets, test conditions, and verification methods, using domain-specific defaults from domain knowledge.
---

# NFR Definition

Domain knowledge for defining measurable, testable non-functional requirements.

## When to Use

- User asks to define NFRs, SLAs, or quality attributes
- Any capability is being specified without performance/quality targets
- Reviewing requirements that lack measurable non-functional criteria

## NFR Structure

Every NFR follows this format:
- **Quality:** The attribute (latency, availability, throughput, accuracy)
- **Target:** Measurable value (p99 < 200ms, 99.95% uptime)
- **Conditions:** When this target applies (peak load, market hours)
- **Measurement:** How to verify (APM dashboard, load test, recon query)
- **Priority:** Must Have / Should Have / Could Have
- **Source:** Research finding, regulation, or SLA that drives this

## Key Principles

- NFRs without measurable targets are opinions, not requirements.
- Load domain defaults from `references/domain-knowledge.md` as starting points.
- Every capability needs at least: latency, availability, and data quality NFRs.
- Conditions matter — "fast" means different things at 10 RPS vs 100k RPS.
- NFRs must be testable before delivery, not discovered in production.
