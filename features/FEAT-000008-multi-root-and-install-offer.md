# `FEAT-000008-UVqkd7cL` — Multi-root workspace support + install-offer

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000008-UVqkd7cL` |
| **Name** | `multi-root-and-install-offer` |
| **Filename** | `FEAT-000008-multi-root-and-install-offer.md` |
| **Status** | Completed |
| **Opened** | 2026-09-06 |
| **Area** | catalyst-host-vscode |
| **Roadmap** | `RM-000008-UVqkd7cL` |
| **Requirement(s)** | `REQ-000008-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Two related gaps in `catalyst-host-vscode`'s `activate()`, both from
the same root cause (it only ever looked at
`workspaceFolders[0]`): a multi-root workspace with more than one
catalyst deployment silently only inspected the first, and a folder
with no `*.catalyst` pointer was silently ignored rather than helped.
This feature makes the extension deployment-aware per folder, and
turns "no deployment found" into an actionable offer to copy a ready
instantiation prompt to the clipboard.

## Motivation

Both gaps were found while using the extension day to day, not from
the original pasted roadmap — genuinely new scope, opened directly
against a new roadmap row (`RM-000008-UVqkd7cL`) rather than one of the seven
original phases.

## Rough scope

In: per-folder deployment resolution/watching/tree grouping/
diagnostics scoping, reacting live to folders added/removed, a
sibling-directory heuristic (falling back to a `catalyst.frameworkPath`
setting) for locating the catalyst framework repo, copying an
instantiation prompt to the clipboard. Out: actually performing
catalyst's instantiation procedure (an agent-driven process per
`BOOTSTRAP.md`, not something this extension can run itself), any
change to `catalyst-core` (`resolveCorpusRoot`/`watchCorpus` are
already per-corpus-root) or `catalyst-host-electron` (already
multi-project).

## Open questions

None specific to this feature.

## Related

`REQ-000008-UVqkd7cL` implements this feature.
