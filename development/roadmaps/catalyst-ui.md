# `RM-NNNNNN` roadmap — catalyst-ui

**Name:** catalyst-ui
**Source:** Catalyst UI — roadmap (pasted 2026-09-05; saved to
`/private/tmp/claude-501/-Users-oliviersteck-sources-catalyst/8631e144-54fe-4680-b59a-dc3dd66b400b/scratchpad/catalyst-ui-roadmap.md`
for ingest)
**Added:** 2026-09-05
**Last updated:** 2026-09-05

## Items

| ID | Title | Description | Status | Linked | Signed-off-by | Notes |
|---|---|---|---|---|---|---|
| `RM-000001-UVqkd7cL` | Phase 1 — Core, no UI | Parser, typed model, global validator, watcher, and protocol types — the headless core every later phase builds on. | Done | REQ-000001-UVqkd7cL | Olivier Steck | Parser, typed model, global validator, watcher, protocol types; ships as a CLI printing the validation report. Exit: synthetic 5× repo passes under 100ms in CI; protocol types published from core. |
| `RM-000002-UVqkd7cL` | Phase 2 — VS Code chain inspector, read-only | Sidebar tree of the four layers, plus a webview for node detail — read-only. | Done | REQ-000002-UVqkd7cL | Olivier Steck | Sidebar tree of the four layers; one webview for node detail. Exit: used daily instead of grepping for IDs. |
| `RM-000003-UVqkd7cL` | Phase 3 — Health board and editor affordances | Validation report as a worklist with CodeLens/gutter marks and click-to-jump, still read-only. | Done | REQ-000003-UVqkd7cL | Olivier Steck | Validation report as a worklist; CodeLens/gutter marks; click-to-jump. Still read-only. Exit: an orphan appears on the board before it would've been noticed by hand. |
| `RM-000004-UVqkd7cL` | Phase 4 — Proposal loop, fix-only | Proposal file format and a fix-only propose-fix action from the health board, reconciled into applied/partial/stale. | Done | REQ-000004-UVqkd7cL | Olivier Steck | Proposal file format, "propose fix" from the health board, pending badges, reconciliation into applied/partial/stale. Exit: one orphan fixed end-to-end with no manual file edits. |
| `RM-000005-UVqkd7cL` | Phase 5 — Authoring composer | Compiles new work items and rules, authored in the UI, into a structured proposal. | Done | REQ-000005-UVqkd7cL | Olivier Steck | New work items and rules as structured intent compiled to a proposal. Exit: a work item created from the UI has a valid, never-reused ID and resolves all links on first parse. |
| `RM-000006-UVqkd7cL` | Phase 6 — Electron host | Mounts the same UI package in Electron, adding multi-project tracking, persistent watch, and a graph view. | Done | REQ-000006-UVqkd7cL | Olivier Steck | Mount the same UI package; add multi-project, persistent watch, and a graph view. Exit: shipped with no changes to `catalyst-ui`. |
| `RM-000007-UVqkd7cL` | Phase 7 — Run monitor | Live run checklist and ledger surfacing agent-side drift before a run completes. | Done | REQ-000007-UVqkd7cL | Olivier Steck | Live checklist and ledger; depends on proposals existing and on agent-side run-state emission (not yet specified). Exit: a drift event is visible in the UI before the run completes. |
| `RM-000008-UVqkd7cL` | VS Code multi-root workspace support + install-offer | Multi-root workspace support plus an install-offer for folders with no catalyst deployment yet. | Done | REQ-000008-UVqkd7cL | Olivier Steck | New scope beyond the original pasted roadmap (not one of its seven phases): `activate()` only ever inspected `workspaceFolders[0]`, so a multi-root workspace with 2+ catalyst deployments silently only showed one, and a folder with no `*.catalyst` pointer was silently ignored. Exit: 2+ deployments open in one workspace each get their own tree section; a folder with no deployment offers to copy a ready instantiation prompt to the clipboard. |
| `RM-000009-UVqkd7cL` | Agent window for running catalyst slash commands | Runs a discovered slash command through the deployment's own agent CLI from a per-project window/terminal. | In progress | REQ-000009-UVqkd7cL | Olivier Steck | New scope beyond the original pasted roadmap: run a discovered `.claude/commands/*.md` slash command through the deployment's own agent CLI from inside each host, rather than a manual copy-paste into an unrelated terminal. Exit: a command run from either host's UI lands in a per-project agent window/terminal, not a shared one that can cross-send into the wrong project's live session. |

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
