# `STEP-000015-UVqkd7cL` — Place detail panels in their project's group

| Field | Value |
|---|---|
| **ID** | `STEP-000015-UVqkd7cL` |
| **Name** | `place-detail-panels-in-project-group` |
| **Filename** | `STEP-000015-place-detail-panels-in-project-group.md` |
| **Parent** | `REQ-000013-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-01 |
| **Closed** | 2026-10-01 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `REQ-000013-UVqkd7cL`.

## Actions performed

- `packages/catalyst-host-vscode/src/panel-groups.ts`: `targetColumn()` — a
  project's first detail panel opens beside the active editor; later ones
  join the group of that project's most recently focused panel (`single`:
  of any project); hidden panels are ignored. `readGrouping()`.
- `extension.ts` `showDetailPanel(key, project, …)`: tracks each panel's
  project and last focus (`onDidChangeViewState`), opens in the computed
  column instead of always `ViewColumn.Beside`; the five callers (node,
  IAM user/role, journal, backlog) pass their corpus root.
- `package.json`: setting `catalyst.detailPanelGroups` (`perProject`
  default, `single`).

## Verification

`src/test/panel-groups.test.ts` (6 tests); host suite 85 passing; tsc,
eslint, prettier clean. `extension.ts` remains untested glue over the
VS Code API, as before; no Extension Host was launched.
