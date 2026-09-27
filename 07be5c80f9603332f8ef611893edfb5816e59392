# catalyst-host-electron rules

Product behavior rules for `packages/catalyst-host-electron` — the
Electron desktop host adapting `catalyst-core`'s protocol to a
multi-project shell and a graph view, and `packages/catalyst-ui`'s
shared React surface mounted inside its renderer. Distinct from
`catalyst-host-vscode-rules.md` (prefix `vscode`), which governs the VS
Code extension's own equivalent surface — the two hosts are siblings,
neither amends the other.

## Contents

- [`DESKTOP`](#desktop) — `electron-DESKTOP-001`

## `DESKTOP`

> **Domain:** `DESKTOP` — see [domains/electron-DESKTOP-multi-project-host-and-graph-view.md](domains/electron-DESKTOP-multi-project-host-and-graph-view.md).

### `electron-DESKTOP-001` Multi-project tracking, persistent watch, and graph view

✅ working. The Electron app tracks a persisted list of
projects (each resolved to its own corpus root the same way
`catalyst-host-vscode` resolves one), running one `watchCorpus`
instance per tracked project concurrently — not just the single
project a VS Code window happens to have open. Selecting a project
shows a graph view of its chain model (nodes grouped by layer, laid out
deterministically rather than via a physics simulation) and, for a
selected node, the same `NodeDetail` component `catalyst-host-vscode`
mounts in its webview, imported unchanged from `catalyst-ui`. Read-only
— no proposal creation or authoring composer in this phase; that reuses
`catalyst-core`'s existing proposal-loop infrastructure
(`core-CONTRACT-002`) later, not redefined here. Targeted by
`REQ-000006`.

Implemented: `packages/catalyst-host-electron/src/{state,graph,detail,
GraphView,main,preload,renderer-entry}.ts(x)` — `state.ts` (persisted
tracked-project list), `graph.ts` (`computeGraphLayout`, deterministic
column-by-kind layout, no physics simulation), `detail.ts` (local
`buildNodeDetail`, same shape as `catalyst-host-vscode`'s own copy —
kept independent rather than a cross-host import, matching how neither
host package exposes its adapter logic for the other today),
`GraphView.tsx` (plain SVG, no graph library), `main.ts`/`preload.ts`
(one persistent `watchCorpus` per tracked project, IPC for
list/add/remove project and node detail), `renderer-entry.tsx` (mounts
`catalyst-ui`'s `NodeDetail` unchanged — no file added to
`packages/catalyst-ui`). Tested: `npm run lint`, `npm run format:check`,
`npm run typecheck`, `npm test` (106 tests total, 16 in this package)
all exit zero; `main.ts`/`preload.ts`/`renderer-entry.tsx` stay thin,
untested glue, same deliberate deferral as both `catalyst-host-vscode`
domains — no real Electron window was launched this session (needs a
display this sandbox doesn't have). Verified end-to-end against this
deployment's own real corpus: `computeGraphLayout` resolves 56 nodes
and 37 edges with every position finite and no two nodes sharing a
position; the renderer bundle (`esbuild`, 142.5kb) and the `tsc` build
both succeed cleanly.

## Known Bugs — Quick Index

*(none yet — no implementation exists to have found bugs in)*
