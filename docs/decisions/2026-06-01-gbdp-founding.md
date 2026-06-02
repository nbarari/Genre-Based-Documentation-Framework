---
genre: Transaction
status: Accepted
impacts: [docs/architecture/protocol.md]
---
# 2026-06-01: Founding of the Genre-Based Documentation Protocol

## Context

Most documentation frameworks treat all docs as equivalent. The result is wikis where decisions, design descriptions, procedures, and standing rules accumulate in unstructured folders. Over time these gather stale content, lose cross-references, and stop being read.

The specific failure mode: ADR-style numbered decision records tend to absorb content that belongs in architecture snapshots (how it works now) and conventions (standing rules). The record of a one-time choice and the living description of current state end up in the same format with no structural difference between them.

## Decision

Establish GBDP: a documentation convention organized by genre. Documents are classified by mutability and intent rather than topic:

- **Snapshot** — edited in place to track current reality
- **Transaction** — dated, immutable, records a single event
- **Artifact** — factual or procedural reference
- **Strategy** — dependency-ordered planning
- **Exploration** — time-bounded pre-decision research

Four operational rules enforce the classification: Differential Rigor (scope determines overhead), Transactional Sync (decisions and snapshots stay linked), Ghost Protocol (delete replaced content from snapshots), and Maturity Lock (no code merges on a proposed decision).

## Consequences

- Contributors assess change class before writing documentation.
- Stale content has a defined removal path rather than accumulating indefinitely.
- Architecture docs reflect current state only — no historical content, no ghost references.
- AI context is well-defined: architecture is current state, decisions are reasoning, both are active context for any agent or contributor working in the repo.

## Apply log

*2026-06-01 — Initial implementation. Added SPEC.md, CONTRIBUTING.md, DEVELOPER.md, MIGRATING.md, genre templates, folder manifests, and docs/conventions/genre-lifecycle.md. AI.md made tool-agnostic with symlink wiring table.*
