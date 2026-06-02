---
genre: Snapshot
status: Stable
refers-to: [README.md, SPEC.md]
---
# GBDP Protocol

## What this is

GBDP is a documentation convention for software repositories. It defines five document genres, four operational rules, and a metadata standard. The complete specification is in `README.md`.

## Structure

| File / Folder | Purpose |
|---|---|
| `README.md` | Full protocol specification |
| `SPEC.md` | Protocol invariants and Definition of Done |
| `CONTRIBUTING.md` | Change class definitions and sync rules |
| `DEVELOPER.md` | How to work with and contribute to this repo |
| `MIGRATING.md` | How to adopt GBDP on an existing repo |
| `AI.md` | Canonical AI context, wired per-tool via symlink |
| `docs/decisions/` | Design choices made while building the protocol |
| `docs/conventions/` | Standing rules the protocol follows |
| `docs/architecture/` | This document |

## Genre summary

| Group | Genre | Mutability | Folders |
|---|---|---|---|
| A | Snapshot | Edited in place | architecture/, conventions/ |
| B | Transaction | Immutable | decisions/, incidents/ |
| C | Strategy | Edited in place | roadmap/ |
| D | Artifact | Edited when facts change | reference/, runbooks/ |
| E | Exploration | Time-bounded | research/ |

## What is not here (and why)

**A validator/linter** — not yet implemented. Enforcement is via code review and the Maturity Lock rule. A CI-runnable linter checking frontmatter completeness and cross-reference integrity is the logical next addition.

**Per-language or per-framework examples** — GBDP is language-agnostic. Examples live in adopting repos, not in the protocol itself.

**A changelog** — `docs/decisions/` is the changelog. No separate `CHANGELOG.md`.

**Version numbers** — the protocol does not use semver. Breaking changes produce a Class 1 decision. Non-breaking additions produce a Class 2 decision.
