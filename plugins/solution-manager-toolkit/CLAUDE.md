# Solution Manager Toolkit

AI-assisted tools for the solution management workflow: user research synthesis, requirements generation, and workshop preparation.

## Directory Structure

```
.claude-plugin/
  plugin.json          # Plugin metadata and version

commands/
  synthesize-research.md   # /synthesize-research command
  generate-requirements.md # /generate-requirements command
  workshop-prep.md         # /workshop-prep command

skills/
  research-synthesizer/SKILL.md    # Research synthesis skill
  requirements-generator/SKILL.md  # Requirements generation skill
  workshop-prep/SKILL.md           # Workshop preparation skill

agents/
  theme-extractor.md              # Agent for parallel theme extraction across sources
  institutional-knowledge-check.md # Senior review agent for gap analysis and blind spots
```

## Versioning

Update all three on every change:
1. `.claude-plugin/plugin.json` — bump version (semver)
2. `CHANGELOG.md` — document changes
3. `README.md` — update component counts
