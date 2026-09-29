# `FEAT-000003-UVqkd7cL` — Health board and editor affordances

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000003-UVqkd7cL` |
| **Name** | `health-board-and-editor-affordances` |
| **Filename** | `FEAT-000003-health-board-and-editor-affordances.md` |
| **Status** | Completed |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-host-vscode |
| **Roadmap** | `RM-000003-UVqkd7cL` |
| **Requirement(s)** | `REQ-000003-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

The validation report as a native VS Code worklist (the Problems panel,
via a `DiagnosticCollection`) instead of a custom view, click-to-jump on
any backtick-quoted id in a corpus file (a `DefinitionProvider`), and a
CodeLens above each node's own heading/field-table summarizing what it
targets/cites, linking through to its detail webview from Phase 2. Still
read-only.

## Motivation

"Editor affordances" reads most naturally as native VS Code extension
points, not more custom UI: diagnostics already give a worklist,
click-to-jump, and gutter marks in one API, and a definition provider is
the idiomatic way to make an id "clickable." Reuses Phase 1's model and
Phase 2's webview command as-is.

## Rough scope

In: a `DiagnosticCollection` refreshed on every watcher update, a
`DefinitionProvider` and a `CodeLensProvider` scoped to the resolved
corpus root's markdown files. Out (this phase): "propose fix" actions
(Phase 4), drift/pending badges (need the proposal loop), a graph view
(Phase 6).

## Open questions

- None specific to this phase.

## Related

`REQ-000003-UVqkd7cL` implements this feature.
