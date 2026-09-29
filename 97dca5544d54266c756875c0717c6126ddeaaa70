# `REQ-000003-UVqkd7cL` — Health board and editor affordances

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000003-UVqkd7cL` |
| **Name** | `health-board-and-editor-affordances` |
| **Filename** | `REQ-000003-health-board-and-editor-affordances.md` |
| **Status** | Completed |
| **Opened** | 2026-09-05 |
| **Targets** | `vscode-HEALTH-000001-UVqkd7cL` |
| **Domain** | `HEALTH` |
| **Feature** | `FEAT-000003-UVqkd7cL` |
| **Steps** | `STEP-000009-UVqkd7cL` |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Surface the validation report as native VS Code diagnostics (a
worklist, click-to-jump, and gutter marks in one API), add a
`DefinitionProvider` so any backtick-quoted id in a corpus markdown
file jumps to its definition, and a `CodeLensProvider` summarizing each
node's own resolved links, opening its detail via the existing
`catalyst.showNodeDetail` command. No new `catalyst-core`/`catalyst-ui`
work needed — reuses Phase 1's model/report and Phase 2's webview
command as-is.

## Acceptance

- Every issue in the watched model's `ValidationReport` appears as a
  diagnostic at its `location`, refreshing on a watcher update.
- An issue with no single `location` (id reuse) gets one diagnostic per
  definition site instead of being dropped.
- Cmd/Ctrl-click (or F12) on any backtick-quoted id inside a corpus
  markdown file jumps to that id's defining location.
- Each node's own heading/field-table gets a CodeLens naming what it
  targets/cites; clicking opens that node's detail webview.
- All three are scoped to the resolved corpus root's markdown files
  only, not the whole workspace.
- Still read-only: no propose-fix actions, no drift/pending badges.

## Notes

Single rule (`vscode-HEALTH-000001-UVqkd7cL`) covers diagnostics, the definition
provider, and CodeLens together — one coherent "editor affordances"
contract, not three separate rules.
