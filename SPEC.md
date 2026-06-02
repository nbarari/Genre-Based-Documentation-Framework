---
genre: Snapshot
status: Stable
---
# Technical Specification

## Invariants

1. The genre taxonomy (Groups A–E) is the structural foundation. Adding or removing a genre is a Class 1 change.
2. The four operational rules are non-negotiable. Changes require a Class 1 decision.
3. The metadata standard (YAML frontmatter) applies to all documentation files.
4. The bootstrapper must produce a working GBDP repo in a single run.
5. `AI.md` is the single source of AI context. Tool-specific files are derived from it, never independently maintained.

## Definition of Done

A change to this protocol is complete when:
1. The relevant Snapshot (`docs/architecture/`) reflects the change.
2. An accepted decision exists in `docs/decisions/` for Class 1/2 changes.
3. The bootstrapper produces the updated structure when run from scratch.
4. `AI.md` is current with the operational rules.
