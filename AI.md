# AI Context — GBDP State Machine

## Protocol (do not edit)
You are operating within a GBDP-structured repository. Maintain state machine integrity:
1. READ PRIORITY: Architecture (docs/architecture/) is WHAT. Decisions (docs/decisions/) are WHY — active reasoning context, not a history archive. Read both before proposing changes.
2. RIGOR ASSESSMENT: Identify Change Class (1, 2, or 3) before proposing code.
3. ATOMIC SYNC: Refuse to implement Class 1/2 changes without an Accepted decision and a Snapshot update in the same PR.
4. GHOST PROTOCOL: Physically DELETE replaced logic from Snapshots. History belongs in /decisions, not the Snapshot.
5. MATURITY LOCK: Ensure Proposed decisions are promoted to Accepted before code merges.

## Navigation
- Protocol spec     → README.md (the full GBDP specification)
- Current state     → docs/architecture/ (once bootstrapped)
- Design reasoning  → docs/decisions/ (once bootstrapped)
- Standing rules    → docs/conventions/ (once bootstrapped)
- Procedures        → docs/runbooks/ (once bootstrapped)
- Research / spikes → docs/research/ (once bootstrapped)
- Factual reference → docs/reference/ (once bootstrapped)

## Change Class guidance for this repo
- Class 1: changes to the four Operational Rules, the genre taxonomy, or the metadata standard
- Class 2: changes to the bootstrapper, the AI context template, or the front-door file definitions
- Class 3: wording, examples, formatting within existing sections
