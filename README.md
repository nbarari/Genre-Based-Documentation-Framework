# Genre-Based Documentation Protocol (GBDP)

## 1. Core Model

A GBDP repository is a structured record of the system's design.

1. **Decisions are immutable.** Design choices are recorded as dated files in `/decisions`. They are never edited after acceptance.
2. **Architecture is the current state.** It reflects what exists now, not what was planned or replaced.
3. **Roadmaps are dependency-ordered.** Tracks define what must be true before the next thing can start.
4. **Metadata is the linkage.** Cross-references keep decisions and snapshots in sync.

---

## 2. Root Files

| File | Role |
| :--- | :--- |
| **SPEC.md** | Invariants: hard constraints and Definition of Done. |
| **DEVELOPER.md** | Setup, commands, and troubleshooting. |
| **CONTRIBUTING.md** | Change classes, sync rules, and governance. |
| **README.md** | High-level description and current status. |
| **AI.md** | AI context. Wired per-tool via symlink. See Section 6. |
| **MIGRATING.md** | How to adopt GBDP on an existing repo with docs. |

---

## 3. Genre Taxonomy (`docs/`)

Organized by **mutability** and **intent**. Every folder contains a `README.md` manifest.

### Group A: Snapshot (Living State)
*Edited in place to reflect current reality. Deleted when the thing it describes no longer exists.*
- `/architecture`: One file per component. **1 component = 1 file.**
- `/conventions`: Standing rules. Edited when the rule changes.

### Group B: Transaction (Record)
*Dated, immutable. Never edited after acceptance. Format: `YYYY-MM-DD-slug.md`.*
- `/decisions`: Design choices.
- `/incidents`: Post-mortems.

### Group C: Strategy
- `/roadmap`: Dependency-ordered tracks.
- `/roadmap/execution-order.md`: Track sequence and current position.

### Group D: Artifact (Fact & Procedure)
- `/reference`: Factual data — API specs, schemas, inventories.
- `/runbooks`: Step-by-step procedures for non-automated tasks.

### Group E: Exploration (Pre-Decision Research)
*Time-bounded. Not a design commitment. Produces a Decision or is abandoned.*
- `/research`: Tool evaluations, spikes, feasibility studies.
- `/research/archive/`: Concluded or abandoned explorations.

---

## 4. Operational Rules

### Rule 1: Differential Rigor
Required rigor is determined by **scope of change**, not preference.

| Class | Scope | Required |
| :--- | :--- | :--- |
| **Class 1** | Invariants (`SPEC.md`) or cross-component logic | Decision + Snapshot update + SPEC sync |
| **Class 2** | Component contracts (interfaces, APIs) | Decision + Snapshot update |
| **Class 3** | Local implementation, fixes | Commit message only |

### Rule 2: Transactional Sync
An `Accepted` decision requires a Snapshot update in the same PR. Decisions and architecture stay in sync.

### Rule 3: Ghost Protocol
Snapshots describe what exists now. When logic is replaced, the old description is deleted. It belongs in `/decisions`, not the architecture.

### Rule 4: Maturity Lock
No code merges on a `Proposed` decision. Decisions are promoted to `Accepted` at merge.

### Rule 5: Diagrams as Code
Architecture diagrams are authored in text (Mermaid/PlantUML) and updated in the same PR as the logic they represent.

---

## 5. Metadata Standard

All documentation includes a YAML frontmatter block:

- **`genre`**: document classification
- **`status`**: lifecycle state (see `docs/conventions/genre-lifecycle.md`)
- **`impacts`**: from a Transaction, links to the Snapshot it changed
- **`refers-to`**: from an Artifact or Snapshot, links to what it explains

```yaml
---
genre: [Snapshot | Transaction | Artifact | Strategy | Exploration]
status: [Proposed | Accepted | Stable | Superseded | Deprecated | Active | Concluded | Abandoned]
impacts: []
refers-to: []
---
```

---

## 6. AI Context

The canonical AI context lives in `AI.md` at the repo root. The bootstrapper generates this file. Wire it once to your tool — all tools read the same content from the same source.

### Wiring `AI.md` to your tool

| Tool | Command |
| :--- | :--- |
| **Claude Code** | `ln -s AI.md CLAUDE.md` |
| **Cursor** | `ln -s AI.md .cursorrules` |
| **GitHub Copilot** | `ln -s AI.md .github/copilot-instructions.md` |
| **Windsurf** | `ln -s AI.md .windsurfrules` |
| **Aider** | Add `--read AI.md` to `.aider.conf.yml` |
| **Any tool** | Paste contents into the system prompt |

If symlinks are unsuitable, a `make ai-sync` target that copies the file achieves the same result.

### Content shape

`AI.md` has two sections: the **Protocol** (fixed — copy verbatim from GBDP and do not edit) and the **Navigation** (fill in per project after bootstrapping).

```markdown
# AI Context — GBDP

## Protocol (do not edit)
You are working in a GBDP-structured repository. Follow these rules:

1. Architecture (docs/architecture/) describes current state. Decisions (docs/decisions/) explain why. Read both before proposing changes — decisions are active context, not a history archive.
2. Identify the change class (1, 2, or 3) before writing code.
3. Do not implement Class 1/2 changes without an accepted decision and a snapshot update in the same PR.
4. Delete replaced logic from architecture docs. It belongs in /decisions, not the snapshot.
5. Do not merge code that depends on a proposed decision. Promote it to accepted first.

## Navigation (fill in per project)
- Current state     → docs/architecture/
- Design reasoning  → docs/decisions/
- Standing rules    → docs/conventions/
- Procedures        → docs/runbooks/
- Research / spikes → docs/research/
- Factual reference → docs/reference/
```

---

## 7. Repository Initializer

Run this to bootstrap a new repository.

```bash
#!/usr/bin/env bash
mkdir -p docs/{architecture,decisions,conventions,roadmap,runbooks,incidents,reference,research/archive}
mkdir -p .github

# SPEC.md — invariants
cat <<'EOF' > SPEC.md
---
genre: Snapshot
status: Stable
---
# Technical Specification

## Invariants
- Class 1/2 changes require a decision record and a Snapshot update.
- All code must pass automated validation before merge.

## Definition of Done
1. Code matches the current Snapshot (docs/architecture/).
2. Snapshot reflects the accepted Decision (docs/decisions/).
3. A passing CLI validator is provided or documented.
EOF

# CONTRIBUTING.md — change classes and sync rules
cat <<'EOF' > CONTRIBUTING.md
# Contributing

## Change Classes
| Class | Scope | Required |
|---|---|---|
| 1 | Invariants or cross-component logic | Decision + Snapshot + SPEC sync |
| 2 | Component contracts | Decision + Snapshot |
| 3 | Local implementation, fixes | Commit message only |

## Sync Rules
1. Class 1/2 changes require a decision record.
2. PRs promoting a decision to Accepted must update the relevant Snapshot.
3. Replaced logic must be deleted from Snapshots — move it to /decisions.
EOF

# DEVELOPER.md — setup and commands
cat <<'EOF' > DEVELOPER.md
# Developer Guide

## Setup
[Fill in: dependencies, install steps]

## Commands
- Build: `make build`
- Verify: `make verify`

## Troubleshooting
[Fill in: common failures and fixes]
EOF

# Roadmap execution order
cat <<'EOF' > docs/roadmap/execution-order.md
# Execution Order

1. [x] Track 0: Protocol initialization
EOF

# AI context
cat <<'EOF' > AI.md
# AI Context — GBDP

## Protocol (do not edit)
You are working in a GBDP-structured repository. Follow these rules:

1. Architecture (docs/architecture/) describes current state. Decisions (docs/decisions/) explain why. Read both before proposing changes — decisions are active context, not a history archive.
2. Identify the change class (1, 2, or 3) before writing code.
3. Do not implement Class 1/2 changes without an accepted decision and a snapshot update in the same PR.
4. Delete replaced logic from architecture docs. It belongs in /decisions, not the snapshot.
5. Do not merge code that depends on a proposed decision. Promote it to accepted first.

## Navigation (fill in per project)
- Current state     → docs/architecture/
- Design reasoning  → docs/decisions/
- Standing rules    → docs/conventions/
- Procedures        → docs/runbooks/
- Research / spikes → docs/research/
- Factual reference → docs/reference/
EOF

# Wire AI.md to your tool (uncomment one):
# ln -s AI.md CLAUDE.md                             # Claude Code
# ln -s AI.md .cursorrules                          # Cursor
# ln -s AI.md .github/copilot-instructions.md       # GitHub Copilot
# ln -s AI.md .windsurfrules                        # Windsurf

# Genre templates
cat <<'EOF' > docs/decisions/_template.md
---
genre: Transaction
status: Proposed
impacts: []
refers-to: []
---
# YYYY-MM-DD: [Short title]

## Context
What situation prompted this decision?

## Decision
What was decided?

## Consequences
What does this enable or constrain?

## Apply log
*Append dated entries when this decision is executed. Record surprises and findings.*
EOF

cat <<'EOF' > docs/architecture/_template.md
---
genre: Snapshot
status: Stable
refers-to: []
---
# [Component name]

## What this is
One paragraph describing the current state of this component.

## What is not here (and why)
Explicit scope exclusions with brief rationale. Prevents future contributors from adding something that was deliberately left out.

## Cross-references
- Decision: [link]
- Convention: [link]
EOF

cat <<'EOF' > docs/runbooks/_template.md
---
genre: Artifact
refers-to: []
validator: [command or link that confirms the procedure succeeded]
---
# [Runbook title]

## When to use this
Trigger condition.

## Prerequisites
What must be true before starting.

## Steps
1. Step one
2. Step two

## Verification
How to confirm success.
EOF

cat <<'EOF' > docs/incidents/_template.md
---
genre: Transaction
status: Accepted
---
# YYYY-MM-DD: [Incident title]

## What happened
Timeline of events.

## Impact
What broke and for how long.

## Root cause
Why it happened.

## Resolution
What fixed it.

## Follow-up
- [ ] [Link to decision produced by this incident]
EOF

cat <<'EOF' > docs/research/_template.md
---
genre: Exploration
status: Active
refers-to: []
---
# [Research topic]

## Question
What are we trying to answer?

## Options considered

| Option | Pros | Cons |
|---|---|---|
| | | |

## Recommendation
Fill in when concluded.

## Output
- Decision: [link when concluded]

---
*Move to research/archive/ when Concluded or Abandoned. Update status accordingly.*
EOF

# Folder manifests
echo "# docs/decisions/\n\nImmutable dated records of design choices. Format: \`YYYY-MM-DD-short-title.md\`.\n\nDo not edit accepted decisions. If superseded, create a new decision and set \`status: Superseded\` on the old one with a link to the replacement." > docs/decisions/README.md
echo "# docs/architecture/\n\nLiving descriptions of current-state design. One file per component.\n\nEdit in place when the component changes. Delete when the component is removed." > docs/architecture/README.md
echo "# docs/conventions/\n\nStanding rules. Edited when the rule changes — not dated, not immutable." > docs/conventions/README.md
echo "# docs/runbooks/\n\nStep-by-step procedures for non-automated tasks." > docs/runbooks/README.md
echo "# docs/incidents/\n\nPost-mortems. Dated, immutable. Link to the decisions they produced." > docs/incidents/README.md
echo "# docs/reference/\n\nFactual data: API specs, schemas, inventories. Updated when the facts change." > docs/reference/README.md
echo "# docs/research/\n\nPre-decision explorations. Move to archive/ when concluded or abandoned." > docs/research/README.md

git init && git add . && git commit -m "chore: initialize GBDP state engine"
```
