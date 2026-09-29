# `REQ-000011-UVqkd7cL` — TEST- entity parsing and display

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000011-UVqkd7cL` |
| **Name** | `test-entity-parsing-and-display` |
| **Filename** | `REQ-000011-test-entity-parsing-and-display.md` |
| **Status** | Completed |
| **Opened** | 2026-09-19 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL`, `vscode-INSPECTOR-000001-UVqkd7cL` |
| **Domain** | `INSPECTOR` |
| **Steps** | `STEP-000003-UVqkd7cL`, `STEP-000004-UVqkd7cL` |
| **Tests** | `TEST-000001-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

The catalyst framework's `TEST-NNNNNN` entity (0.30.0, `Rules-of-Rules.md`
§22 — a fourth rule-targeting development-artifact type alongside
`BUG-`/`REQ-`/`HK-` that may additionally, independently, optionally name
`(0,n)` `REQ-NNNNNN` and `(0,n)` `STEP-NNNNNN` it verifies) reached this
deployment's own `.criterion` via `/sync-framework`, but `catalyst-core`'s
parser had no idea the type existed and the Chain Inspector couldn't show
it — the same gap `REQ-000010-UVqkd7cL` closed for `STEP-`, now repeated
for `TEST-`. This requirement extends the typed chain model to parse
`tests/tests.md` + `tests/*.md` as a fourth `DevArtifactType` (`"test"`),
resolve a test's `Requirements`/`Steps` fields into forward graph edges
toward whichever `REQ-`/`STEP-` it names, and surface tests in the VS Code
Chain Inspector.

## Acceptance

- `catalyst-core` parses `tests/tests.md` + `tests/*.md` into
  `DevArtifactNode`s of a new `"test"` `DevArtifactType`, with
  `requirements`/`steps` optional array fields read from a test's own
  `Requirements`/`Steps` fields.
- `graph.ts` adds forward edges from a test to whichever `REQ-`/`STEP-`
  it names; an unresolvable id is caught by the existing generic
  `dangling-reference` check, no bespoke validator logic needed.
- The VS Code host (`catalyst-host-vscode`) shows a "Tests" sub-section
  under "Dev Artifacts", a passing/failing/blocked/proposed status
  glyph, and a dedicated icon.
- A test nests under both its parent requirement and its parent step in
  the sidebar tree (many-to-many — a test can appear under more than one
  parent, or under none), resolved via the chain model's reverse edges,
  the same mechanism `REQ-000010-UVqkd7cL` introduced for a requirement's
  steps.
- Full test coverage across `catalyst-core` (parser/graph/validator) and
  `catalyst-host-vscode` (tree/detail/label), plus one `catalyst-ui`
  `NodeDetail` case.

## Notes

Targets the same two rules `REQ-000010-UVqkd7cL` targeted
(`core-CONTRACT-000001-UVqkd7cL` for the parser,
`vscode-INSPECTOR-000001-UVqkd7cL` for the tree) — this is an extension
of both rules' existing scope, not a new rule, the same treatment
`REQ-000010-UVqkd7cL` itself received for the `STEP-` rollout. Verified:
`npx tsc --build --force` clean; full monorepo `npm test`: `catalyst-core`
189/189, `catalyst-host-electron` 16/16 (unaffected), `catalyst-host-vscode`
79/79, `catalyst-ui` 25/25 — 309 tests total, all green, zero regressions.
`npm run lint` clean.
