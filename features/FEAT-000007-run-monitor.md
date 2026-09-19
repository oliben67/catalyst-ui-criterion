# `FEAT-000007-UVqkd7cL` — Run monitor

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000007-UVqkd7cL` |
| **Name** | `run-monitor` |
| **Filename** | `FEAT-000007-run-monitor.md` |
| **Status** | shipped |
| **Opened** | 2026-09-06 |
| **Area** | catalyst-core, catalyst-host-vscode |
| **Roadmap** | `RM-000007-UVqkd7cL` |
| **Requirement(s)** | `REQ-000007-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

The last roadmap item: a `runs/RUN-NNNNNN.md` file format an external
agent emits and mutates in place as it works (unlike a proposal, never
created or edited by the UI), and a "Runs" tree section in
`catalyst-host-vscode` showing each run's live checklist and ledger,
with drift (`⚠️`) visible on the section label as soon as it's written
— before the run itself completes.

## Motivation

Closes the roadmap's own last open question (the agent-side run-state
format) now that proposals — the other prerequisite — have shipped and
a format/host decision has been made. Completes the roadmap's four
listed surfaces (chain inspector, health board, proposal loop, run
monitor).

## Rough scope

In: `runs/*.md` parsing and `hasDrift` (`catalyst-core`), a read-only
"Runs" tree section with per-run checklist/ledger expansion
(`catalyst-host-vscode`). Out: any UI-driven run creation or mutation
(only the external agent writes a run file, mirroring how only the
agent advances a proposal's `Status`), independent verification of a
step's `drift` claim (self-reported, same posture as a proposal's
`Expectations`), and any change to `catalyst-host-electron` (this
phase's host decision is VS Code only).

## Open questions

None specific to this feature — the roadmap's own remaining open
questions (a proposal staleness timeout, whether Phases 1–7 get their
own catalyst work-item IDs) belong to other, already-shipped items, not
this one.

## Related

`REQ-000007-UVqkd7cL` implements this feature. Builds on `FEAT-000004-UVqkd7cL`'s
`proposals/` precedent for the uniform artifact-type deployment shape.
