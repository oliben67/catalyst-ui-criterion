# `REQ-000017-UVqkd7cL` — Track the entity in the chain tree

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000017-UVqkd7cL` |
| **Name** | `track-entity-in-chain-tree` |
| **Filename** | `REQ-000017-track-entity-in-chain-tree.md` |
| **Status** | Completed |
| **Opened** | 2026-10-02 |
| **Targets** | `vscode-INSPECTOR-000001-UVqkd7cL` |
| **Domain** | `INSPECTOR` |
| **Steps** | `STEP-000020-UVqkd7cL` |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

When navigating through links within an entity (`REQ-000014-UVqkd7cL`),
the entity opened is revealed and selected in the chain inspector tree;
likewise when a node's detail panel is brought to the front — like the
explorer's auto-reveal of the active file. Setting
`catalyst.trackEntityInTree` (default on).

## Acceptance

- Every tree item has a stable `id` (its parent path plus a structural
  key) and the provider implements `getParent`; the view is a
  `TreeView` (`createTreeView`).
- Opening an entity from a link, or focusing a node's detail panel,
  reveals that node: its first, shallowest occurrence in its deployment
  (the section that lists it), selected, without moving focus.
- Only while the chain inspector is visible: it never opens the sidebar.
- `catalyst.trackEntityInTree: false` turns it off.

## Notes

Pure pieces (item keys, unique ids, the bounded breadth-first search) in
`tree-ids.ts`, unit-tested.
