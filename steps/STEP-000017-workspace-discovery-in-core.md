# `STEP-000017-UVqkd7cL` — Workspace discovery and the scope rule in catalyst-core

| Field | Value |
|---|---|
| **ID** | `STEP-000017-UVqkd7cL` |
| **Name** | `workspace-discovery-in-core` |
| **Filename** | `STEP-000017-workspace-discovery-in-core.md` |
| **Parent** | `REQ-000015-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-01 |
| **Closed** | 2026-10-01 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

`catalyst-core` `workspace.ts`: deployments in a folder, the scope rule, ignored folders.

## Actions performed

`packages/catalyst-core/src/workspace.ts`, exported from `index.ts`:
`ignoreLines`, `hasPointer`, `optedOut`, `governs` (the kernel's
`scope.py` rule, ported), `owningDeployment` (deepest root, then
`governs`), `isIgnoredFolder` (relative or absolute entries),
`findDeployments` (breadth-first to `maxDepth` 4, skipping `.git`,
`.criterion`, `node_modules`, build folders, opted-out and ignored
directories; nested deployments kept).

## Verification

`src/test/workspace.test.ts` (4 tests) passing.
