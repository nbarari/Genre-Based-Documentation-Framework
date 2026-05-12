# Genre-Based Documentation Framework (GBDF)

## 1. Core Philosophy: The Repo as a State Machine
This repository is managed as a verifiable state machine. 
1.  **Decisions are Transactions (The Log):** Every design change is recorded as a dated, immutable transaction.
2.  **Architecture is the Snapshot (The State):** The current truth is a high-fidelity "materialized view" of the code.
3.  **The Metadata is the Linkage:** YAML headers allow humans and AI to differentiate between history and reality.

---

## 2. The Front-Door Interfaces (Root Level)
Every repository must maintain four top-level files to serve as the entry points for different intents.

| File | Type | Principle |
| :--- | :--- | :--- |
| **SPEC.md** | **The Anchor** | **Declarative Invariants**: The technical constitution, hard constraints, and tech stack. |
| **DEVELOPER.md** | **The Cockpit** | **Procedural Operations**: Setup, commands, and **Fire Suppression** (Troubleshooting). |
| **CONTRIBUTING.md** | **Social Contract** | **Governance**: The rules for Design Tiers, the Sync Protocol, and PR norms. |
| **README.md** | **Marketing** | **The Billboard**: High-level value proposition and current product status. |

---

## 3. The Genre Taxonomy (`docs/`)
The `docs/` folder is organized by **mutability** (how often it changes) and **intent**.

### Group A: Snapshot (Living Truth)
*Updated only to reflect the current reality. Narratives and text-based diagrams.*
*   `docs/architecture/`: Current design. (e.g., `auth-flow.md`, `data-model.md`).
*   `docs/conventions/`: Team rules and standards. (e.g., `naming.md`).

### Group B: Transaction (Forensic History)
*Dated, immutable records of design evolution. Never deleted.*
*   `docs/decisions/`: Choice records (ADRs). Format: `YYYY-MM-DD-slug.md`.
*   `docs/incidents/`: Post-mortems of system failure and durable fixes.

### Group C: Strategy (Strategic Intent)
*   `docs/roadmap/`: **Capability-Based Planning**. Dependency tracks, not calendar tasks.
*   `docs/roadmap/execution-order.md`: The "Playlist" for building the project from scratch.

### Group D: Fact & Procedural (Artifacts)
*   `docs/reference/`: Strictly factual data (API specs, schemas).
*   `docs/runbooks/`: Step-by-step procedures for manual tasks.

### Group E: Ephemeral (Discovery)
*   `docs/research/`: Spikes and discovery. Once a spike is codified into an ADR, the research file is archived or deleted to prevent context poisoning.

---

## 4. The Operational Rules

### Rule 1: The Transactional Sync
Any PR that adds an `Accepted` Design Transaction (ADR) **must** contain a modification to the Snapshot (`/architecture`) or the Anchor (`SPEC.md`) in the same commit history.

### Rule 2: Radical Excision (The Ghost Protocol)
Snapshots must be "ghost-free." When logic is replaced, the old description **must be deleted**. History is archived in the Ledger (`/decisions`); the Snapshot is for the present.

### Rule 3: The Maturity Lock
Merging code is the act of accepting design. No code may be merged into `main` that relies on a `Proposed` ADR. ADRs must be promoted to `Accepted` upon merge.

### Rule 4: Visual Twin (Diagrams-as-Code)
Architecture diagrams must be authored in text (Mermaid/PlantUML). Diagrams are code: if the logic they represent changes, the diagram must be updated in the same PR.

### Rule 5: Traceability Headers
All documentation must include a YAML header for context-pruning:
*   **`impacts`**: Link from a **Transaction** to the Snapshot it mutated.
*   **`refers-to`**: Link from an **Artifact** or **Snapshot** to the file it explains/depends on.

---

## 5. AI Identity (Instructions for Agents)
*Paste this into `.cursorrules`, `CLAUDE.md`, or your System Prompt.*

```markdown
# Role: System Architect
You are a component of the GBDF State Machine. Enforce the protocol:
1. READ PRIORITY: Use docs/architecture/ for state. Use docs/decisions/ only for history.
2. ATOMIC SYNC: Refuse to implement Tier 1/2 changes without an 'Accepted' ADR and a Snapshot update.
3. GHOST PROTOCOL: Physically DELETE replaced logic from Snapshots; do not use "Note: this was replaced."
4. MATURITY LOCK: Ensure all 'Proposed' ADRs are promoted to 'Accepted' if code is being merged.
```

---

## 6. Repository Initializer Script
*Run this to bootstrap a new GBDF-compliant repo.*

```bash
#!/usr/bin/env bash
mkdir -p docs/{architecture,decisions,conventions,roadmap,runbooks,incidents,reference,research/archive}
cat <<EOF > SPEC.md
# TECHNICAL SPECIFICATION (The Anchor)
---
genre: Snapshot
status: Stable
---
## 1. Technical Invariants
- 
## 2. Definition of Done (DoD)
1. Code matches Snapshot (/architecture).
2. Snapshot reflects Decision (/decisions).
3. Passing CLI Validator provided.
EOF

cat <<EOF > CONTRIBUTING.md
# CONTRIBUTING
## The Sync Protocol
- PRs adding 'Accepted' Decisions MUST update the Snapshot/Anchor.
- Old logic MUST be excised from Snapshots.
- No code merged on 'Proposed' ADRs.
EOF

echo "# Execution Order" > docs/roadmap/execution-order.md
echo "1. [x] Capability: Protocol Initialization" >> docs/roadmap/execution-order.md
git init && git add . && git commit -m "chore: initialize GBDF State Engine"
```
