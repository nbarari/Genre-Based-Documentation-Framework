# Migrating an existing repo to GBDP

Most existing repos have documentation but no genre boundaries. The migration is an audit — classifying what you have reveals what was conflated and what is stale.

## Steps

### 1. Run the bootstrapper

Run the bash block from `README.md` Section 7. It creates the genre folders and templates alongside your existing files without touching them.

### 2. Classify each existing doc

For each file, assign a genre:

| If the document... | Genre | Destination |
|---|---|---|
| Describes how something works now | Snapshot | `docs/architecture/component-name.md` |
| Records a one-time design choice | Transaction | `docs/decisions/YYYY-MM-DD-slug.md` |
| Establishes a standing rule | Snapshot | `docs/conventions/rule-name.md` |
| Post-mortem of an outage or failure | Transaction | `docs/incidents/YYYY-MM-DD-slug.md` |
| Tool comparison or spike | Exploration | `docs/research/topic.md` |
| Step-by-step procedure | Artifact | `docs/runbooks/task-name.md` |
| API spec, schema, inventory | Artifact | `docs/reference/name.md` |

The classification step is where you discover that most existing doc folders conflate all of these. That discovery is the value of the migration.

### 3. Move and rename

- Decisions: rename to `YYYY-MM-DD-slug.md`. Use the actual date of the decision if known; use today's date if not.
- Architecture: one file per component, named after the component.
- Conventions: no date prefix — they are living documents.

### 4. Update cross-references

Fix any links broken by the moves. Add `impacts` and `refers-to` frontmatter fields to link decisions to the snapshots they changed.

### 5. Write a migration decision

Create `docs/decisions/YYYY-MM-DD-adopted-gbdp.md` explaining why you migrated and what the old structure was. One paragraph is enough.

### 6. Wire AI.md

Follow the wiring table in `README.md` Section 6.

---

## Handling numbered ADRs (ADR-0001 style)

Numbered ADRs usually mix decisions and architecture descriptions in one format. For each:

- If it records a one-time choice → `docs/decisions/`
- If it describes how something works now → `docs/architecture/`
- If it establishes a standing rule → `docs/conventions/`

Keep a resolver table in `docs/decisions/README.md` mapping old ADR numbers to new paths. This preserves citation links in commit history and PR references.

```markdown
## Legacy ADR resolver

| ADR | New location |
|---|---|
| ADR-0001 | docs/decisions/2024-01-15-monorepo-layout.md |
| ADR-0002 | docs/architecture/auth-service.md |
```

---

## Common situations

**"We have a big wiki with no structure."**
Treat each wiki page as a doc to classify. Most wiki pages are either architecture docs or runbooks that drifted into an unstructured format. Start with the pages that are most frequently referenced — those are the ones most likely to be stale and most worth cleaning up first.

**"We have ADRs but also a separate docs/ folder."**
Classify everything. ADRs often contain architecture content that should be extracted to a Snapshot. The docs/ folder often contains decisions that were never formally recorded. The migration forces the split.

**"We have nothing."**
Run the bootstrapper, wire AI.md, and start writing. The first decision record can be "adopted GBDP."
