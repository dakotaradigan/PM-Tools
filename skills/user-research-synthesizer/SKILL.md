---
name: user-research-synthesizer
description: This skill should be used when synthesizing raw user research (interview notes, workshop transcripts, survey responses, stakeholder meeting notes) into structured problem statements, persona cards, theme matrices, and prioritized findings. Triggers on "synthesize research", "analyze interviews", "extract themes", "build personas", "problem statements from research", or when raw qualitative/quantitative user research needs structured analysis.
allowed-tools: Read, Glob, Grep, Write, Agent, Bash
user-invocable: true
---

# User Research Synthesizer

This skill transforms raw user research inputs into structured, actionable artifacts that accelerate the solution management workflow.

## Supported Input Types

- Interview notes (1:1 or group)
- Workshop transcripts and card sorting results
- Survey responses (quantitative + open-ended)
- Stakeholder meeting notes
- Support tickets or feedback logs
- Usability test observations

## Core Process

### Phase 1: Intake & Inventory

1. Scan the provided files or directory for research inputs
2. Catalog each source: type, date, participant role/segment, format
3. Present the inventory to the user for confirmation before proceeding

### Phase 2: Theme Extraction

For each input source:

1. **Extract observations** — Pull out distinct observations, complaints, requests, and behaviors. Tag each with:
   - Source (which participant/document)
   - Segment (role, team, persona group)
   - Sentiment (positive, negative, neutral)
   - Topic area (assign a short label)

2. **Cluster into themes** — Group observations that share a common root cause or topic. Each theme gets:
   - Theme name (concise, descriptive)
   - Description (1-2 sentences)
   - Frequency (how many sources mention it)
   - Segments affected (which roles/personas)
   - Representative quotes (2-3 verbatims)
   - Severity signal (blocking, painful, annoying, nice-to-have)

3. **Surface contradictions** — Flag where different segments disagree or have conflicting needs. These are critical design tensions that require explicit tradeoff decisions.

### Phase 3: Persona Synthesis

Build persona cards from the research. Each persona card includes:

```
## [Persona Name] — [Role Title]

**Segment:** [e.g., Front Office / Trading]
**Archetype:** [1-line summary of who this person is]

### Goals
- [Primary goal]
- [Secondary goals]

### Pain Points
- [Ranked by severity]

### Current Workarounds
- [What they do today to cope]

### Key Quote
> "[Most representative verbatim from research]"

### Success Metric
- [How this persona would measure if the solution works]
```

Generate personas from the data — do not invent personas that aren't supported by the research. Typically 3-5 personas emerge from a research round.

### Phase 4: Problem Statement Generation

For each major theme, generate a structured problem statement:

```
## Problem Statement: [Theme Name]

**Who:** [Affected personas/segments]
**Situation:** [Current state — what they deal with today]
**Problem:** [The specific pain or gap]
**Impact:** [Business/operational/user consequence]
**Evidence:** [X of Y participants mentioned this; survey score; quote]

### How Might We...
- [HMW question 1 — framing the opportunity]
- [HMW question 2 — alternative framing]
```

Rank problem statements by: frequency across sources, severity of impact, and breadth of affected segments.

### Phase 5: Output Artifacts

Generate the following outputs:

1. **Research Summary** (`research-summary.md`)
   - Executive summary (3-5 sentences)
   - Methodology (sources, dates, participant counts)
   - Top findings (ranked)
   - Theme matrix (theme x segment heatmap in markdown table)
   - Recommended next steps

2. **Persona Cards** (`personas.md`)
   - All persona cards in the format above

3. **Problem Statements** (`problem-statements.md`)
   - All problem statements ranked by priority
   - Contradictions and design tensions section

4. **Raw Theme Matrix** (`theme-matrix.md`)
   - Theme x Source cross-reference table showing which themes appeared in which sources
   - Useful for traceability and audit

## Output Conventions

- Write all outputs to a `synthesis/` subdirectory relative to the input files
- Use markdown formatting throughout
- Include source attribution for every claim (which interview, which survey question)
- Do not invent data — every finding must trace to an input source
- Flag low-confidence findings where evidence is thin (single source, ambiguous statement)
- When quantitative data (survey scores, NPS) is available, include it alongside qualitative themes

## Quality Checks

Before presenting final outputs:

- [ ] Every theme links to at least 2 sources (unless flagged as low-confidence)
- [ ] Every persona maps to real participants, not archetypes
- [ ] Problem statements include specific evidence, not generalities
- [ ] Contradictions between segments are called out, not smoothed over
- [ ] HMW questions are genuinely open-ended, not solution-prescriptive
- [ ] No findings were invented or inferred beyond what the data supports
