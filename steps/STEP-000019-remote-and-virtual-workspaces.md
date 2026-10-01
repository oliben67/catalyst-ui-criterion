# `STEP-000019-UVqkd7cL` — Remote and virtual workspaces

| Field | Value |
|---|---|
| **ID** | `STEP-000019-UVqkd7cL` |
| **Name** | `remote-and-virtual-workspaces` |
| **Filename** | `STEP-000019-remote-and-virtual-workspaces.md` |
| **Parent** | `REQ-000016-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-01 |
| **Closed** | 2026-10-01 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `REQ-000016-UVqkd7cL`.

## Actions performed

- `catalyst-core` `discover.ts`: `workingCopyState()` — `reachable` (with
  the path), `dangling` (with the symlink's target) or `missing`; exported.
- `catalyst-host-vscode` `remote.ts`: `environmentLabel()` (from
  `vscode.env.remoteName`), `devcontainerMount()` (a bind mount of the
  target at the same path, so the symlink resolves), `unreachableAdvice()`
  (dev container: mount or share; elsewhere: share or install here).
- `extension.ts`: non-`file` workspace folders are skipped; a deployment
  whose working copy is not reachable is reported once, with **Copy
  devcontainer mount** and **Share with /criterion create** (through the
  trust-guarded agent path), instead of silently skipped; the status bar
  tooltip names the environment.
- `package.json`: `extensionKind: ["workspace"]`,
  `capabilities.virtualWorkspaces.supported: false`.

## Verification

`discover.test.ts` (+1), `remote.test.ts` (3); all workspaces pass (core
245, electron 16, vscode host 91, ui 35) — except `perf.test.ts`'s
wall-clock limit, which fails intermittently under load (measured: 30–37
ms cold, ~20 ms warm, against 100 ms); unrelated to this change, left as
is. tsc, eslint, prettier clean. Not run in an actual remote, WSL or
container Extension Host.
