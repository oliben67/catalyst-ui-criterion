# `REQ-000013-UVqkd7cL` — Detail panels: at most one editor group per project

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000013-UVqkd7cL` |
| **Name** | `detail-panels-one-group-per-project` |
| **Filename** | `REQ-000013-detail-panels-one-group-per-project.md` |
| **Status** | Completed |
| **Opened** | 2026-10-01 |
| **Targets** | `vscode-INSPECTOR-000001-UVqkd7cL` |
| **Domain** | `INSPECTOR` |
| **Steps** | `STEP-000015-UVqkd7cL` |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Every detail panel (node, IAM user/role, journal, backlog) opens with
`ViewColumn.Beside`: beside the *focused* group, so a click made from
inside a detail panel creates yet another editor group — one more column
per click. Panels of one project belong together: at most one editor
group per project, each panel a tab in it; optionally one single group
for every project (`catalyst.detailPanelGroups`: `perProject` default,
or `single`). Roadmap `RM-000028-UVqkd7cL`.

## Acceptance

- The first detail panel of a project opens beside the active editor;
  every later one of the same project opens as a tab in the group that
  project's panels are in (following the panel the user last focused, if
  they were moved).
- `single`: every project's panels share one group.
- Re-opening an entity still reveals its existing panel (unchanged).

## Notes

Pure placement logic in `panel-groups.ts` (unit-tested); `extension.ts`
stays glue.
