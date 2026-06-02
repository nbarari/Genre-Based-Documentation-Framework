# Genre-Based Documentation Protocol (GBDP)

## 1. Core Philosophy: The Repo as a State Machine
This repository is a **Digital Twin** of the system’s logic. 
1.  **Decisions are Transactions:** Immutable design deltas recorded in `/decisions`.
2.  **Architecture is the Snapshot:** The current "Source of Truth." It is high-fidelity and "ghost-free."
3.  **Roadmaps are Capability-Based:** Logical dependency tracks that define "Value Unlocks."
4.  **The Metadata is the Linkage:** Cross-references ensure the ledger always balances.

---

## 2. The Front-Door Interfaces (Root Level)

| File | Intent | Primary Role |
| :--- | :--- | :--- |
| **SPEC.md** | **The Anchor** | **Declarative Invariants**: Tech stack, hard constraints, and DoD. |
| **DEVELOPER.md** | **The Cockpit** | **Procedural Operations**: Setup, commands, and Fire Suppression. |
| **CONTRIBUTING.md** | **The Protocol** | **Governance**: Change Classes, Sync Rules, and Social Contract. |
| **README.md** | **The Billboard** | **Marketing**: High-level value and current status. |

---

## 3. The Genre Taxonomy (`docs/`)

Organized by **Mutability** and **Intent**. Every folder contains a `README.md` manifest.

### Group A: Snapshot (Living State)
*Updated only to reflect the current reality. Narratives and text-based diagrams.*
*   `/architecture`: Narrative design. **1 component = 1 identifier.**
*   `/conventions`: Standing rules (Naming, Modularity, Refactor triggers).

### Group B: Transaction (History)
*Dated, immutable records of design evolution. Flat structure: `YYYY-MM-DD-slug.md`.*
*   `/decisions`: Design Transactions (ADRs).
*   `/incidents`: Forensic Transactions (Post-mortems of state failure).

### Group C: Strategy (Strategic Intent)
*   `/roadmap`: **Capability-Based Tracks**. (e.g., "Persistence Layer").
*   `/roadmap/execution-order.md`: The project "Playlist" (Track 0 is the Protocol).

### Group D: Artifacts (Fact & Procedural)
*   `/reference`: Factual data (API specs, schemas, design exports).
*   `/runbooks`: Manual procedures for non-automated tasks.

---

## 4. Operational Rules

### Rule 1: Differential Rigor (Change Classes)
The required rigor is determined by the **scope of mutation**, not the developer's preference.

| Class | Target | Requirement |
| :--- | :--- | :--- |
| **Class 1** | Invariants in `SPEC.md` or cross-component logic. | **ADR + Snapshot + Anchor Sync** |
| **Class 2** | Component Contracts (Interfaces/API). | **ADR + Snapshot Sync** |
| **Class 3** | Local Implementation (Private logic/Fixes). | **Commit Message Only (Fast Path)** |

### Rule 2: The Transactional Sync (Double-Entry)
An `Accepted` Decision **requires** a Snapshot update in the same PR. You cannot change the ledger without updating the balance.

### Rule 3: Radical Excision (The Ghost Protocol)
Snapshots must be a mirror of the code *now*. When logic is replaced, the old description **must be deleted**. History belongs in the Ledger (`/decisions`), not the Snapshot.

### Rule 4: The Maturity Lock
Merging code is the act of accepting design. No code may be merged into `main` that relies on a `Proposed` ADR. ADRs must be promoted to `Accepted` upon merge.

### Rule 5: Visual Twin (Diagrams-as-Code)
Architecture diagrams must be authored in text (Mermaid/PlantUML) and updated in the same PR as the logic they visualize.

---

## 5. Metadata Standard
All documentation must include a YAML header for context-pruning:
*   **`impacts`**: Link from a **Transaction** to the Snapshot it mutated.
*   **`refers-to`**: Link from an **Artifact** or **Snapshot** to the file it explains/depends on.

```yaml
---
genre: [Snapshot | Transaction | Artifact | Capability]
status: [Proposed | Accepted | Stable | Superseded | Deprecated]
impacts: [Link to Snapshot]
refers-to: [Link to Snapshot or SPEC Anchor]
validator: [CLI command or persistent Artifact link]
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
# AI Context — GBDP State Machine

## Protocol (do not edit)
You are operating within a GBDP-structured repository. Maintain state machine integrity:
1. READ PRIORITY: Architecture (docs/architecture/) is WHAT. Decisions (docs/decisions/) are WHY — active reasoning context, not a history archive. Read both before proposing changes.
2. RIGOR ASSESSMENT: Identify Change Class (1, 2, or 3) before proposing code.
3. ATOMIC SYNC: Refuse to implement Class 1/2 changes without an Accepted decision and a Snapshot update in the same PR.
4. GHOST PROTOCOL: Physically DELETE replaced logic from Snapshots. History belongs in /decisions, not the Snapshot.
5. MATURITY LOCK: Ensure Proposed decisions are promoted to Accepted before code merges.

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
*Run this to bootstrap a repository as a validated State Engine.*

```bash
#!/usr/bin/env bash
mkdir -p docs/{architecture,decisions,conventions,roadmap,runbooks,incidents,reference,research/archive}
mkdir -p .github

# Initialize the Anchor
cat <<EOF > SPEC.md
# TECHNICAL SPECIFICATION (The Anchor)
---
genre: Snapshot
status: Stable
---
## 1. Technical Invariants
- All code must pass automated validation.
- Class 1/2 changes require ADR + Snapshot Sync.

## 2. Definition of Done (DoD)
1. Code matches Snapshot (/architecture).
2. Snapshot reflects Decision (/decisions).
3. Passing CLI Validator provided.
EOF

# Initialize the Social Contract
cat <<EOF > CONTRIBUTING.md
# CONTRIBUTING
## The Sync Protocol
1. Class 1/2 changes REQUIRE an ADR.
2. PRs adding 'Accepted' Decisions MUST update the Snapshot.
3. Old logic MUST be excised from Snapshots.
EOF

# Initialize the Cockpit
cat <<EOF > DEVELOPER.md
# DEVELOPER OPERATIONS (The Cockpit)
## 1. Standard Commands
- Build: \`make build\`
- Verify: \`make verify\`
## 2. Troubleshooting
- Health Check: [Command]
EOF

# Initialize the Playlist
echo "# Execution Order" > docs/roadmap/execution-order.md
echo "1. [x] Capability: Protocol Initialization" >> docs/roadmap/execution-order.md

# Initialize the AI context
cat <<'EOF' > AI.md
# AI Context — GBDP State Machine

## Protocol (do not edit)
You are operating within a GBDP-structured repository. Maintain state machine integrity:
1. READ PRIORITY: Architecture (docs/architecture/) is WHAT. Decisions (docs/decisions/) are WHY — active reasoning context, not a history archive. Read both before proposing changes.
2. RIGOR ASSESSMENT: Identify Change Class (1, 2, or 3) before proposing code.
3. ATOMIC SYNC: Refuse to implement Class 1/2 changes without an Accepted decision and a Snapshot update in the same PR.
4. GHOST PROTOCOL: Physically DELETE replaced logic from Snapshots. History belongs in /decisions, not the Snapshot.
5. MATURITY LOCK: Ensure Proposed decisions are promoted to Accepted before code merges.

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

git init && git add . && git commit -m "chore: initialize GBDP state engine"
```
