# `STEP-000018-UVqkd7cL` — Workspace-aware extension host

| Field | Value |
|---|---|
| **ID** | `STEP-000018-UVqkd7cL` |
| **Name** | `workspace-aware-host` |
| **Filename** | `STEP-000018-workspace-aware-host.md` |
| **Parent** | `REQ-000015-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-01 |
| **Closed** | 2026-10-01 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

`extension.ts`: a deployment per pointer, the install offer's opt-outs, `catalyst.ignoredFolders`, Workspace Trust, the status bar item.

## Actions performed

- `extension.ts`: `resolveFolder` registers one deployment per pointer
  `findDeployments` finds (nested ones included; named `<folder>` or
  `<folder>/<path>`), `teardownFolder` removes them all;
  `setupDeployment` and `offerToSyncKernel` take a `{ name, path }` target
  instead of a workspace folder. No install offer for an opted-out or
  ignored folder; the offer gains **Never offer here** (writes an empty
  `.catalystignore`) and **Not in this workspace** (adds the folder to
  `catalyst.ignoredFolders`, workspace scope). Changing the setting, or
  granting trust, re-resolves every folder. A status bar item names the
  deployment owning the active editor's file (`owningDeployment`), with
  its kernel version; a click opens its backlog.
- Workspace Trust: `package.json` `capabilities.untrustedWorkspaces`
  `limited`; untrusted, no install or sync offer, and `resolveAndInvoke`
  (`agent-bridge.ts`) refuses agent commands.
- `package.json`: setting `catalyst.ignoredFolders` (resource scope).

## Verification

The pure pieces are tested in `catalyst-core` (`workspace.test.ts`); all
workspaces pass (244, 16, 88, 35), tsc, eslint, prettier clean;
`extension.ts` remains glue, not run in an Extension Host. The
`perf.test.ts` timing limit (100 ms) failed once under the parallel full
run and passed alone (5/5) and on the rerun — load, not this change.
