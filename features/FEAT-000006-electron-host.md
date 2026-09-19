# `FEAT-000006-UVqkd7cL` — Electron host

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000006-UVqkd7cL` |
| **Name** | `electron-host` |
| **Filename** | `FEAT-000006-electron-host.md` |
| **Status** | shipped |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-host-electron |
| **Roadmap** | `RM-000006-UVqkd7cL` |
| **Requirement(s)** | `REQ-000006-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

The second host: `packages/catalyst-host-electron`, still a one-line
stub, mounts `catalyst-ui`'s shared React surface unchanged, adds
multi-project tracking with a persistent `watchCorpus` per project, and
a graph view of the chain model — the one surface the roadmap withheld
from the VS Code host until this phase.

## Motivation

Proves `catalyst-core`'s protocol is genuinely host-agnostic (the
roadmap's own exit criterion: shipped with no changes to `catalyst-ui`)
and delivers the graph view, deliberately deferred until a host that
can afford its layout cost across more than one project at a time.

## Rough scope

In: Electron main/preload/renderer, a persisted tracked-project list,
one concurrent `watchCorpus` instance per tracked project, a
deterministic (non-physics) graph layout, and `NodeDetail` reused from
`catalyst-ui` for the selected node. Out: the run monitor (`RM-000007-UVqkd7cL`,
separately deferred — its own agent run-state format is still
unspecified), packaging/installers/code-signing/auto-update, proposal
creation or the authoring composer from this host (read-only, same as
`catalyst-host-vscode` was at its own equivalent phase).

## Open questions

None specific to this feature — the roadmap's remaining open questions
(Phase 7's run-state format, a proposal staleness timeout, whether
Phases 1–7 get their own catalyst work-item IDs) belong to other items,
not this one.

## Related

`REQ-000006-UVqkd7cL` implements this feature.
