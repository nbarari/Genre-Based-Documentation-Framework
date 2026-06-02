# AI Context — GBDP

## Protocol (do not edit)
You are working in a GBDP-structured repository. Follow these rules:

1. Architecture (`docs/architecture/`) describes current state. Decisions (`docs/decisions/`) explain why. Read both before proposing changes — decisions are active context, not a history archive.
2. Identify the change class (1, 2, or 3) before writing code.
3. Do not implement Class 1/2 changes without an accepted decision and a snapshot update in the same PR.
4. Delete replaced logic from architecture docs. It belongs in `/decisions`, not the snapshot.
5. Do not merge code that depends on a proposed decision. Promote it to accepted first.

## Navigation
- Protocol spec     → README.md
- Current state     → docs/architecture/
- Design reasoning  → docs/decisions/
- Standing rules    → docs/conventions/
- Procedures        → docs/runbooks/
- Research / spikes → docs/research/
- Factual reference → docs/reference/

## Change Class guidance for this repo
- Class 1: genre taxonomy, operational rules, metadata standard
- Class 2: bootstrapper, templates, AI context content, root file definitions
- Class 3: wording, examples, formatting within existing sections
