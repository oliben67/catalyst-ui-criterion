# `FEAT-000001` — Core: parser, typed model, validator, watcher

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000001` |
| **Filename** | `FEAT-000001-core-parser-model-validator-watcher.md` |
| **Status** | shipped |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-core |
| **Roadmap** | `RM-000001` |
| **Requirement(s)** | `REQ-000001` |
| **Signed-off-by** | Olivier Steck |

## Description

`catalyst-core` — TypeScript, no DOM. Parses the corpus (rules, dev
artifacts, work items), builds a typed chain model connecting them,
runs global validation (orphans, ID reuse, dangling refs), and watches
files for changes. Ships first as a CLI printing the validation report,
with no UI attached yet.

## Motivation

Every later phase (VS Code inspector, health board, proposal loop,
Electron host, run monitor) is a consumer of this same core — the
protocol types it exposes are the contract everything else builds
against. Getting the parse/model/validate/watch loop right, fast, and
correctly typed before any UI exists is what makes every later phase
tractable.

## Rough scope

In: corpus parsing, typed chain model, global validator (orphans, ID
reuse, dangling refs — inherently global, not incremental), file
watcher with debounce/coalesce and single-flight cancellation, the
message protocol types consumed by later host packages. Out (this
phase): any UI, any host adapter, incremental validation (only
revisited if the CI perf assertion fails), direct writes (never
planned — proposals are the design).

## Open questions

- None specific to this phase beyond the roadmap's own open questions
  (agent run-state format, proposal timeout, whether phases get their
  own catalyst work-item IDs) — none of which block Phase 1's own
  scope.

## Related

`REQ-000001` implements this feature.
