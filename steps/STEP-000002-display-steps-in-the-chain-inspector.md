# `STEP-000002-UVqkd7cL` — Display steps in the Chain Inspector

| Field | Value |
|---|---|
| **ID** | `STEP-000002-UVqkd7cL` |
| **Name** | `display-steps-in-the-chain-inspector` |
| **Filename** | `STEP-000002-display-steps-in-the-chain-inspector.md` |
| **Requirement** | `REQ-000010-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-09-19 |
| **Closed** | 2026-09-19 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Surface `StepNode`s (from `STEP-000001-UVqkd7cL`) in the VS Code Chain
Inspector: a top-level Steps section, plus a requirement expanding to
show its own steps as children — the UI half of `REQ-000010-UVqkd7cL`.

## Actions performed

- `packages/catalyst-host-vscode/src/tree.ts`: added `"step"` to
  `TreeSectionKind`, `SECTION_LABELS` ("Steps"), `SECTION_ORDER`, and the
  `buildTreeSections` grouping condition; added a dedicated status-glyph
  branch to `getNodeStatusGlyph` for `planned`/`in-progress`/`done`/
  `abandoned` (the generic fallback didn't recognize any of them); added
  `"step"` to `getNodeUser`'s `signedOffBy`-bearing kinds.
- `packages/catalyst-host-vscode/src/extension.ts`: added `step` entries
  to `SECTION_ICON_NAMES`, `SECTION_ENTITY_TYPES`, `ENTITY_TYPE_LABELS`,
  and `nodeIconName`; added `hasStepChildren`/`stepChildrenFor` methods
  to `ChainInspectorProvider` (resolving a requirement's steps via
  `model.reverseEdges`), wired into `getTreeItem` (collapsible state) and
  `getChildren` (the new `"node"` branch — previously unhandled, always
  fell through to `[]`).
- New icons: `resources/icons/{light,dark}/step.svg` (a simple
  checklist glyph — no icon for this concept existed yet).
- `packages/catalyst-ui`: no changes needed — `NodeDetail.tsx`'s generic
  field/section rendering and `<NodeList>` (`upstream`/`downstream`)
  already render a step's own detail view and list a requirement's steps
  under "Produces (downstream)" once the graph edge exists.
- Added test coverage: 1 case in `tree.test.ts` (Steps section
  grouping), 1 in `detail.test.ts` (a requirement's downstream includes
  its steps, resolved via `reverseEdges`), 1 in `catalyst-ui`'s
  `NodeDetail.test.ts` (a step renders in a requirement's Produces list).

## Verification

`npx tsc --build --force` clean across every workspace; full monorepo
`npm test`: catalyst-core 181/181, catalyst-host-electron 16/16,
catalyst-host-vscode 73/73, catalyst-ui 24/24 — zero regressions.
`npm run lint` clean.

## Related

`STEP-000001-UVqkd7cL` (the parsing half, in `catalyst-core`).
