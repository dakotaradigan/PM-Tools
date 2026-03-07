---
name: solution-work:piplan
description: Prepare for SAFe PI Planning with feature breakdowns, WSJF prioritization, dependency mapping, and PI objectives
allowed-tools: Read, Glob, Grep, Write, Bash
user-invocable: true
---

# PI Planning Preparation

Prepare artifacts for a SAFe Program Increment planning ceremony.

## Steps

1. **Load references** — Read `references/domain-knowledge.md` for SAFe/PI Planning terminology and roles. Read `references/team-context.md` for team-specific stakeholders, team ownership areas, and org context if available.

2. **Gather inputs** — Check for existing artifacts: `requirements/user-stories.md`, `requirements/nfrs.md`, `data-model/canonical-entities.md`, `api-contracts/endpoints.md`. These provide the backlog of work to plan. If no artifacts exist, ask the user to describe the features.

3. **Break features into PI-sized increments** — Each feature must fit within one PI (8-12 weeks, typically 4-5 sprints). If a feature is too large, decompose it into smaller features. Classify each as:
   - **Business Feature** — Delivers user-visible value
   - **Enabler** — Technical infrastructure, exploration, or compliance work

4. **Score with WSJF** — For each feature, prompt the user to estimate:
   - User-Business Value (1-20)
   - Time Criticality (1-20)
   - Risk Reduction / Opportunity Enablement (1-20)
   - Job Size (1-20)
   - WSJF = (Value + Time Criticality + RR/OE) / Job Size

5. **Map dependencies** — Identify cross-team and cross-system dependencies for each feature. Flag features with more than 2 dependencies as high-risk.

6. **Draft PI Objectives** — For each team, draft SMART PI Objectives (committed and uncommitted) based on the prioritized feature list.

7. **Identify risks** — Categorize using ROAM: Resolved, Owned, Accepted, Mitigated. Flag unmitigated risks.

8. **Write outputs** — Write to `pi-planning/`:
   - `pi-planning/feature-backlog.md` — Prioritized features with WSJF scores
   - `pi-planning/dependency-map.md` — Cross-team dependency matrix
   - `pi-planning/pi-objectives.md` — Draft PI Objectives per team
   - `pi-planning/risks.md` — ROAM-categorized risk register

9. **Update solution state** — If `solution_state.md` exists, update the `pi_plan` artifact status.

## Important

- Features must fit in one PI. If not, split until they do.
- WSJF is the prioritization framework — don't skip it or substitute opinion.
- Dependencies are risks. The goal is to minimize them, not just list them.
- Distinguish committed vs uncommitted PI Objectives — overcommitting destroys trust.
- Enablers compete for capacity. They don't get free passes.
