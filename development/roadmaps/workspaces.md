# `RM-NNNNNN` roadmap — workspaces

**Name:** workspaces
**Source:** design discussion 2026-10-01: VS Code workspaces, detail groups, entity links
**Added:** 2026-10-01
**Last updated:** 2026-10-01

## Items

| ID | Title | Description | Status | Linked | Signed-off-by | Notes |
|---|---|---|---|---|---|---|
| `RM-000028-UVqkd7cL` | Detail panels: at most one editor group per project | Entity detail panels open as tabs in their project's editor group instead of a new group per click; a setting can unite every project's panels in one single group. | Not triaged | `REQ-000013-UVqkd7cL` | Olivier Steck | |
| `RM-000029-UVqkd7cL` | Entity references are links, with a hover | IDs in a rendered entity are links that open the referred entity (in its project's group); hovering shows its name and a short description. Optionally the same in the text editor. | Not triaged | `REQ-000014-UVqkd7cL` | Olivier Steck | |
| `RM-000030-UVqkd7cL` | Workspace-aware extension | Discover nested deployments in a workspace folder; catalyst.ignoredFolders; 'never offer catalyst here' on the install prompt (writes the kernel opt-out marker); Workspace Trust; status bar and Problems panel per deployment. | Not triaged | `REQ-000015-UVqkd7cL` | Olivier Steck | |
| `RM-000031-UVqkd7cL` | Remote, WSL and dev containers | Resolve the computed working-copy location and run the CLI on the remote side; disable cleanly in virtual workspaces. | Not triaged | *(none)* | Olivier Steck | |

## Status values

- **Not triaged** — ingested; no `FEAT-`/`REQ-` for it yet.
- **Triaged** — a `FEAT-NNNNNN` exists for this item (see its `Roadmap` field).
- **In progress** — the linked `FEAT-` was promoted to a `REQ-NNNNNN` that is not yet done.
- **Done** — the linked `REQ-NNNNNN` is complete.

## Source context not captured as items

The source document also locks several architectural decisions (three
packages/one protocol, agent-mediated writes only, full-reparse
indexing, file-based proposal transport — see its "Decisions locked"
table and "Architecture" section) and lists things deliberately
deferred (graph view until Phase 6, incremental validation, direct UI
writes) plus three open questions (Phase 7's agent run-state format, a
proposal staleness timeout, whether Phases 1–7 get their own catalyst
work-item IDs). These are supporting context for the seven phase items
above, not separate roadmap rows — re-read the source document directly
for them; `/roadmap-update` can promote any of these to a tracked row
later if a human decides one is worth its own `RM-NNNNNN`.

## How this file is maintained

- `/roadmap-add <name> <file>` creates this file (this template, once)
  and parses `<file>` into one `RM-NNNNNN` row per distinct item it
  identifies (`Not triaged`, globally next ID across every named
  roadmap — never reused, same as `FEAT-NNNNNN`), `Signed-off-by` set per
  `CODE-OF-CONDUCT.md` §2.
- `/roadmap-update <name> <file>` re-reads `<file>` as the new full,
  authoritative version of this roadmap: adds rows for new items,
  updates matched rows' `Title`/`Notes` (matched by title/description
  similarity — ask the user rather than guessing when ambiguous), and
  flags in `Notes` (never deletes) any row whose item no longer appears
  in the new file. Updates `Source`/`Last updated` above.
- `/roadmap-merge <name> <update file>` treats `<update file>` as a
  partial delta, not the full roadmap: only adds/updates the rows it
  actually contains, with the same matching rule as `-update`. Does not
  compare against or flag rows the delta doesn't mention, and does not
  change `Source` — only `Last updated`.
- `/roadmap-remove <name>` deletes this file and its `roadmaps.md` entry
  outright **only if no row's `Linked` field is set**. If any row is
  linked to a `FEAT-`/`REQ-`, deleting would break that cross-reference
  (`Rules-of-Rules.md` §4's "never delete, retire in place" principle
  applies here too) — instead it adds the `Retired` field above, marks
  this roadmap `retired` in `roadmaps.md`, and leaves every row and ID
  exactly as they are, resolvable, just excluded from `/show-backlog`'s
  active Roadmap section going forward.
- A row stays `Not triaged` until a human decides it's worth tracking
  inside catalyst, at which point `/create-feature` opens its `FEAT-NNNNNN`
  (citing this row's `RM-NNNNNN` ID in the feature's own `Roadmap` field).
- From there, the normal `FEAT-` → `REQ-` promotion applies
  (`Rules-of-Rules.md` §9/§10, `INVARIANTS.md` INV-9); this file's
  `Status`/`Linked` columns always mirror whichever artifact is currently
  linked, refreshed by `/show-backlog` — never edited here directly.
