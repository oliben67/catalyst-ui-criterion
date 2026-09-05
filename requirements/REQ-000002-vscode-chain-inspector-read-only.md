# `REQ-000002` — VS Code chain inspector, read-only

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000002` |
| **Filename** | `REQ-000002-vscode-chain-inspector-read-only.md` |
| **Status** | done |
| **Opened** | 2026-09-05 |
| **Targets** | `vscode-INSPECTOR-001` |
| **Domain** | `INSPECTOR` |
| **Feature** | `FEAT-000002` |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `packages/catalyst-host-vscode`'s real `activate()`: resolve
the opened project's catalyst deployment from its `<name>.catalyst`
pointer file, watch it via `catalyst-core`'s `watchCorpus`, and expose a
sidebar tree (grouped by layer) plus a node-detail webview mounting
`catalyst-ui`'s shared React surface. Extends `catalyst-core` with the
small pieces this needs (corpus discovery, a richer watcher callback,
the node-detail protocol payload) without reopening `core-CONTRACT-001`,
which is already closed.

## Acceptance

- Opening a project with no `<name>.catalyst` pointer shows a graceful
  empty state, not an error.
- Opening catalyst-ui's own repo (which has `catalyst-ui.catalyst`)
  resolves and watches its real `.criterion` deployment.
- The sidebar tree groups nodes into dev artifacts / rules / rules of
  rules / domains / features, refreshing on a watcher update.
- Selecting a node opens a webview showing its own fields plus resolved
  upstream (justified by) and downstream (produces) node lists.
- No editing, no proposals, no live-pushed webview updates in this
  phase — read-only.

## Notes

Targets `vscode-INSPECTOR-001` only, even though part of the
implementation (corpus discovery) lands in `packages/catalyst-core` —
that addition has no independent product meaning yet, so it isn't a
second rule of its own.
