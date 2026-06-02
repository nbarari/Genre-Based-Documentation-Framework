# Contributing

## Change Classes

| Class | Scope | Required |
|---|---|---|
| **1** | Genre taxonomy, operational rules, metadata standard, SPEC.md invariants | Decision + Snapshot update + SPEC sync |
| **2** | Bootstrapper, templates, AI.md content, root file definitions | Decision + Snapshot update |
| **3** | Wording, examples, formatting within existing sections | Commit message only |

When unsure, treat the change as Class 2.

## Sync Rules

1. Class 1/2 changes require a decision record in `docs/decisions/` before code merges.
2. PRs promoting a decision to `Accepted` must update the relevant Snapshot in the same PR.
3. Replaced content must be deleted from Snapshots — it belongs in `/decisions`, not the architecture.

## Decision record format

```
docs/decisions/YYYY-MM-DD-short-title.md
```

Use the template at `docs/decisions/_template.md`. Set `status: Proposed` when drafting, `status: Accepted` at merge.

## What does not need a decision

Class 3 changes (wording, examples, formatting) go straight to a PR with a clear commit message. No decision record required.
