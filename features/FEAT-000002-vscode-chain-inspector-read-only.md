# `FEAT-000002-UVqkd7cL` — VS Code chain inspector, read-only

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000002-UVqkd7cL` |
| **Name** | `vscode-chain-inspector-read-only` |
| **Filename** | `FEAT-000002-vscode-chain-inspector-read-only.md` |
| **Status** | Completed |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-host-vscode, catalyst-ui |
| **Roadmap** | `RM-000002-UVqkd7cL` |
| **Requirement(s)** | `REQ-000002-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

A VS Code extension sidebar showing the chain model's layers (dev
artifacts, rules, rules of rules, domains, features — work items excluded,
none active in this deployment) as a tree, and a webview panel showing one
selected node's detail: its own fields plus what it's justified by
(upstream) and what it produces (downstream). Read-only — no editing, no
proposals yet.

## Motivation

VS Code first because the webview boundary forces the core↔UI message
protocol to be real, with no packaging or auto-update cost while it's
being proven out. Everything else (health board, proposal loop, Electron
host) builds on the same `catalyst-ui` surfaces and the same protocol.

## Rough scope

In: a `TreeDataProvider`-backed sidebar view grouped by layer, a
`WebviewPanel` showing one node's detail on selection, resolving which
catalyst deployment to inspect from the opened project's own
`<name>.catalyst` pointer file (dogfooding: opening catalyst-ui itself
inspects its own real corpus). Out (this phase): editing, proposals,
drift/pending badges (those need the proposal loop, Phase 4), a graph
view (deferred to Phase 6 per the roadmap), live-pushed webview updates
(reopening the panel refreshes it instead).

## Open questions

- None specific to this phase.

## Related

`REQ-000002-UVqkd7cL` implements this feature.
