# `REQ-000001-UVqkd7cL` — catalyst-core: parser, model, validator, watcher

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000001-UVqkd7cL` |
| **Name** | `catalyst-core-parser-model-validator-watcher` |
| **Filename** | `REQ-000001-catalyst-core-parser-model-validator-watcher.md` |
| **Status** | done |
| **Opened** | 2026-09-05 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL` |
| **Domain** | `CONTRACT` |
| **Feature** | `FEAT-000001-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `packages/catalyst-core`: the corpus parser, the typed chain
model it builds, the global validator that runs on every reparse, and
the file watcher with debounce/coalesce and single-flight cancellation
— the full contract `core-CONTRACT-000001-UVqkd7cL` describes. This is the first
requirement opened against `catalyst-core-rules.md`, and the first real
application work in this repository (everything before this was
tooling scaffolding, `env-*`).

## Acceptance

- Parser builds the typed chain model from a full corpus reparse.
- Global validator catches orphaned artifacts, rules without meta-rule
  backing, ID reuse, and dangling references.
- Watcher debounces/coalesces changes in a 150–200ms trailing window,
  with single-flight cancellation on a change landing mid-parse.
- Protocol types are published from `catalyst-core` for later packages
  to consume.
- Ships as a CLI printing the validation report (roadmap Phase 1's own
  exit criterion: a synthetic 5× repo passes under 100ms in CI).

## Notes

Targets `core-CONTRACT-000001-UVqkd7cL` directly — the rule and this requirement
were authored together, since no prior product rule document existed
for catalyst-ui before this.
