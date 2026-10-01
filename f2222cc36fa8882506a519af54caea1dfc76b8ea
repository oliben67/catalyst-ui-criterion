# `STEP-000020-UVqkd7cL` — Reveal the tracked entity in the tree

| Field | Value |
|---|---|
| **ID** | `STEP-000020-UVqkd7cL` |
| **Name** | `reveal-tracked-entity` |
| **Filename** | `STEP-000020-reveal-tracked-entity.md` |
| **Parent** | `REQ-000017-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-02 |
| **Closed** | 2026-10-02 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `REQ-000017-UVqkd7cL`.

## Actions performed

- `catalyst-host-vscode` `tree-ids.ts`: `itemKey()` (a node by its ID, a
  deployment by its corpus root, a section or group by its kind/id/name —
  structural, so ids survive a label's count changing), `childId()` (parent
  id + key, `#n` for a repeat among siblings), `breadthFirst()` (bounded,
  shallowest match first).
- `extension.ts`: `ChainInspectorProvider` gives every item a stable `id`
  and remembers its parent (`getParent`); `findNode()` returns a node's
  first, shallowest occurrence in its deployment. The view is a `TreeView`
  (`createTreeView`); `revealNode()` selects a node without moving focus,
  only while the view is visible and `catalyst.trackEntityInTree` is on.
  A node panel coming to the front, and an entity opened from a link,
  reveal it.
- `package.json`: setting `catalyst.trackEntityInTree` (default `true`).

## Verification

`src/test/tree-ids.test.ts` (3 tests); all workspaces pass (245, 16, 94,
35); tsc, eslint, prettier clean. `extension.ts` remains glue: the reveal
itself was not run in an Extension Host.
