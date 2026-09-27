# `FEAT-000004` — Proposal loop, fix-only

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000004` |
| **Filename** | `FEAT-000004-proposal-loop-fix-only.md` |
| **Status** | shipped |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-core, catalyst-host-vscode |
| **Roadmap** | `RM-000004` |
| **Requirement(s)** | `REQ-000004` |
| **Signed-off-by** | Olivier Steck |

## Description

The first write path: a `proposals/PROP-NNNNNN.md` file format (Intent,
Targets, Expectations, Constraints, reconciliation `Status`), a
"Propose fix" Quick Fix on any health-board diagnostic that creates one
targeting the affected node, and pending-badge display on any node
targeted by an open (non-`applied`) proposal. The UI only ever creates
and displays proposals — it never edits governed files itself; an agent
reads a proposal separately and performs the real fix.

## Motivation

Proves the write loop on the easiest case (a fix with an obvious
expectation) before Phase 5 reuses the same mechanism for harder,
authoring-shaped intent.

## Rough scope

In: the proposal file format and parser, `nextProposalId`/
`openProposalsByTarget`, the Quick Fix action, a proposals tree section,
pending indicators. Out: automatic `stale`-timeout detection (the
roadmap's own open question, not resolved here — `stale` stays a valid,
manually-set status), any UI-driven state transition (an agent, not the
UI, moves a proposal from `proposed` onward), drift badges (need actual
applied-proposal history to be meaningful).

## Open questions

- Proposal timeout for the `stale` state (roadmap's own open question,
  inherited unresolved).

## Related

`REQ-000004` implements this feature.
