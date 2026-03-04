---
name: requirements-generator
description: This skill should be used when generating structured requirements (user stories, acceptance criteria, NFRs) from synthesized problem statements and persona cards. Transforms research insights into implementation-ready requirements.
---

# Requirements Generator

This skill provides domain knowledge for translating synthesized user research into structured requirements.

## When to Use

- Synthesized problem statements exist and need to become actionable requirements
- User asks to "generate requirements", "write user stories", "define acceptance criteria"
- Moving from discovery/research phase to execution/build phase

## Output Artifacts

1. **User Stories** — As a [persona], I want [action], so that [outcome]. MoSCoW prioritized.
2. **Acceptance Criteria** — Given/When/Then format, happy path + edge cases.
3. **Non-Functional Requirements** — Performance, data quality, security, scalability. Only what's evidenced.
4. **Dependency Map** — Implementation ordering based on story dependencies.

## Key Principles

- Requirements trace to problem statements which trace to research. Full chain.
- Do not generate requirements for problems not surfaced in research.
- Flag assumptions explicitly.
- NFRs must be measurable (not "fast" but "< 200ms p95 latency").
- MoSCoW prioritization based on frequency and severity from research, not gut feel.
