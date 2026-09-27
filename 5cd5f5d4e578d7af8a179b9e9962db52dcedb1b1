# `REQ-000010-UVqkd7cL` — STEP- entity parsing and display

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000010-UVqkd7cL` |
| **Name** | `step-entity-parsing-and-display` |
| **Filename** | `REQ-000010-step-entity-parsing-and-display.md` |
| **Status** | done |
| **Opened** | 2026-09-19 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL`, `vscode-INSPECTOR-000001-UVqkd7cL` |
| **Domain** | `INSPECTOR` |
| **Steps** | `STEP-000001-UVqkd7cL`, `STEP-000002-UVqkd7cL` |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

The catalyst framework's `STEP-NNNNNN` entity (0.29.0, `Rules-of-Rules.md`
§21 — one concrete unit of implementation work performed toward a
requirement) reached this deployment's own `.criterion` via
`/sync-framework`, but `catalyst-core`'s parser had no idea the type
existed and the Chain Inspector couldn't show it — the extension was
blind to a real part of the governed corpus. This requirement extends
the typed chain model to parse `steps/`, validate a step's `Requirement`
cross-reference the same way any other dangling reference is caught, and
surfaces a requirement's own steps as children in the sidebar tree.

## Acceptance

- `catalyst-core` parses `steps/steps.md` + `steps/*.md` into `StepNode`s
  (own `NodeKind`), registered/on-disk reconciled the same way
  requirements and features already are.
- A step's `Requirement` field becomes a real graph edge; an
  unresolvable one is caught by the existing generic `dangling-reference`
  check, no bespoke validator logic needed beyond a step-specific
  `orphaned-artifact` check for a missing `Requirement` field or a
  registered/on-disk mismatch.
- The Chain Inspector tree shows a top-level **Steps** section, and a
  requirement with at least one step becomes expandable, listing its
  steps as children (resolved via the chain model's reverse edges).
- A step's own node-detail view renders through the existing generic
  field/section rendering — no bespoke webview component needed — and a
  requirement's detail view lists its steps under "Produces (downstream)"
  for free, once the graph edge exists.
- Full test coverage mirroring the existing requirement/feature parsing,
  graph, and validator test suites.

## Notes

Targets the same two rules a chain-inspector extension has touched
before (`core-CONTRACT-000001-UVqkd7cL` for the parser,
`vscode-INSPECTOR-000001-UVqkd7cL` for the tree) — this is an extension
of both rules' existing scope, not a new rule, the same treatment
`REQ-000008-UVqkd7cL` gave `vscode-INSPECTOR-000001-UVqkd7cL` for
multi-root support.
