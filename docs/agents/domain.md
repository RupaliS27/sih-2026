# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

## Before exploring, read these

- **`CONTEXT.md`** at the repo root: defines the ubiquitous domain vocabulary for the Crop Health System.
- **`docs/adr/`**: architectural decisions on hardware, system boundaries, and active learning.
- **`docs/specs/`**: technical specifications, particularly `sih-2026-crop-health-spec.md`.

## File structure

Single-context repo:

```
/
├── CONTEXT.md                    ← ubiquitous domain language
├── docs/
│   ├── adr/                      ← architectural decision records
│   ├── specs/                    ← feature specifications
│   └── agents/                   ← agent configuration and tracker maps
└── src/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in `CONTEXT.md`. Don't drift to synonyms the glossary explicitly avoids.
