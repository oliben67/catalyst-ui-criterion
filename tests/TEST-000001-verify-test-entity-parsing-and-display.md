# `TEST-000001-UVqkd7cL` — Verify TEST- entity parsing and display

A development artifact like `BUG-`/`REQ-`/`HK-`: always carries its own
`Targets`/`Domain`, vetted the same way (`Rules-of-Rules.md` §1
conflict check, `rules-of-development.md` §1 — no development without a
targeted rule). `Requirements`/`Steps` are additional, independent,
optional `(0,n)` links to whichever `REQ-`/`STEP-` this test verifies —
see `Rules-of-Rules.md` §22.

| Field | Value |
|---|---|
| **ID** | `TEST-000001-UVqkd7cL` |
| **Name** | `verify-test-entity-parsing-and-display` |
| **Filename** | `TEST-000001-verify-test-entity-parsing-and-display.md` |
| **Status** | passing |
| **Opened** | 2026-09-19 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL`, `vscode-INSPECTOR-000001-UVqkd7cL` |
| **Domain** | `INSPECTOR` |
| **Requirements** | `REQ-000011-UVqkd7cL` |
| **Steps** | `STEP-000003-UVqkd7cL`, `STEP-000004-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Verifies that `REQ-000011-UVqkd7cL`'s `TEST-NNNNNN` parsing/graph/tree/
detail work actually holds: `catalyst-core` parses `tests/tests.md` +
`tests/*.md` as a fourth `DevArtifactType`, resolves a test's
`Requirements`/`Steps` fields into forward graph edges, and
`catalyst-host-vscode` surfaces a "Tests" sub-section under "Dev
Artifacts" with a status glyph, a dedicated icon, and correct nesting
under both a test's parent requirement and parent step. This is the
first real `TEST-NNNNNN` instance in this deployment, dogfooding the
entity being deployed the same way `REQ-000010-UVqkd7cL`/`STEP-000001-
UVqkd7cL`/`STEP-000002-UVqkd7cL` dogfooded `STEP-NNNNNN`.

## Procedure

- `packages/catalyst-core/src/test/parser.test.ts` — parses a `test`
  dev-artifact with/without `Requirements`/`Steps`, confirming the
  fields land on `DevArtifactNode` correctly.
- `packages/catalyst-core/src/test/graph.test.ts` — confirms forward
  edges are built from a test node to every `REQ-`/`STEP-` its
  `requirements`/`steps` fields name.
- `packages/catalyst-core/src/test/validator.test.ts` — confirms an
  unresolvable `Requirements`/`Steps` id on a test is caught by the
  existing generic `dangling-reference` check.
- `packages/catalyst-host-vscode/src/test/tree.test.ts` — confirms the
  "Tests" sub-section renders under "Dev Artifacts" and a test nests
  under both its parent requirement and parent step.
- `packages/catalyst-host-vscode/src/test/treeLabel.test.ts` — confirms
  the passing/failing/blocked/proposed status glyph and dedicated icon
  render correctly per test status.
- `packages/catalyst-host-vscode/src/test/detail.test.ts` — confirms a
  requirement's/step's downstream list includes a linked test, resolved
  via `reverseEdges`.
- `packages/catalyst-ui/src/NodeDetail.test.ts` — confirms a test node
  renders through the existing generic field/section rendering.

Run via each package's own `npm test` (or the monorepo root's `npm
test` to run every workspace in one pass).

## Expected outcome

Every listed test file passes, with zero regressions in each package's
pre-existing suite.

## Actual outcome

All green: `catalyst-core` 189/189, `catalyst-host-electron` 16/16
(unaffected), `catalyst-host-vscode` 79/79, `catalyst-ui` 25/25 — 309
tests total, zero regressions. `npx tsc --build --force` clean across
every workspace; `npm run lint` clean.

## Related

`REQ-000011-UVqkd7cL`, `STEP-000003-UVqkd7cL`, `STEP-000004-UVqkd7cL`,
`REQ-000010-UVqkd7cL` (the `STEP-` precedent this rollout mirrors).
