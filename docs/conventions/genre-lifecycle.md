---
genre: Snapshot
status: Stable
refers-to: [README.md]
---
# Genre lifecycle and status transitions

## Status values

| Status | Meaning | Valid for |
|---|---|---|
| `Proposed` | Drafted, not yet accepted | Transaction |
| `Accepted` | Merged and binding | Transaction |
| `Stable` | Current and accurate | Snapshot, Artifact |
| `Superseded` | Replaced by another document | Any |
| `Deprecated` | No longer relevant, kept for reference | Any |
| `Active` | Research in progress | Exploration |
| `Concluded` | Research complete, produced a Decision | Exploration |
| `Abandoned` | Research stopped without a Decision | Exploration |

## Valid transitions

**Transaction** (decisions, incidents)
```
Proposed → Accepted    on merge, per Maturity Lock
Accepted → Superseded  when a newer decision replaces it
```

**Snapshot** (architecture, conventions)
```
Stable → Stable        edited in place when reality changes
Stable → Superseded    when the component or rule is removed
```

**Exploration** (research)
```
Active → Concluded     research complete; link the output Decision in the document
Active → Abandoned     stopped; note why
```

## What status is not

`Stable` means the document accurately describes current reality, not that the thing it describes is finished. A Snapshot of a half-built component is `Stable` if the description is accurate.

`Accepted` on a decision means it was merged and is binding — not that the implementation is complete. The Apply log section tracks execution.

## Conventions have no status

Convention documents are living Snapshots. They do not carry a status field — they are either current (in the folder) or removed. If a convention is superseded, replace its content and note the change in a decision.
