# `TEST-000002-UVqkd7cL` — Verify minimum framework version enforcement

A development artifact like `BUG-`/`REQ-`/`HK-`: always carries its own
`Targets`/`Domain`, vetted the same way (`Rules-of-Rules.md` §1
conflict check, `rules-of-development.md` §1 — no development without a
targeted rule). `Requirements`/`Steps` are additional, independent,
optional `(0,n)` links to whichever `REQ-`/`STEP-` this test verifies —
see `Rules-of-Rules.md` §22.

| Field | Value |
|---|---|
| **ID** | `TEST-000002-UVqkd7cL` |
| **Name** | `verify-minimum-framework-version-enforcement` |
| **Filename** | `TEST-000002-verify-minimum-framework-version-enforcement.md` |
| **Status** | passing |
| **Opened** | 2026-09-20 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL`, `vscode-ONBOARDING-000002-UVqkd7cL` |
| **Domain** | `ONBOARDING` |
| **Requirements** | `REQ-000012-UVqkd7cL` |
| **Steps** | `STEP-000005-UVqkd7cL`, `STEP-000006-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Verifies that `REQ-000012-UVqkd7cL`'s minimum-version work actually
holds: `catalyst-core` correctly parses and evaluates a version
specifier (`>=`/`<=`/`==`/`!=`/`>`/`<`), `REQUIRED_FRAMEWORK_VERSION`
is genuinely described as a specifier rather than a bare number, and
`meetsRequiredFrameworkVersion` treats an unreadable `version.txt` as
satisfying the requirement rather than a false failure.

## Procedure

- `packages/catalyst-core/src/test/versioning.test.ts` — parses every
  supported operator, tolerates surrounding whitespace, throws on a
  specifier with no recognized operator or a missing version; evaluates
  `>=`/`<=`/`==`/`!=`/`>`/`<` against real version pairs.
- `packages/catalyst-core/src/test/discover.test.ts` — confirms
  `REQUIRED_FRAMEWORK_VERSION` itself matches the specifier pattern (not
  a bare number); `meetsRequiredFrameworkVersion` returns `true` at/above
  the floor, `false` below it, and `true` for `null` (can't safely
  compare).

Run via each package's own `npm test` (or the monorepo root's `npm
test` to run every workspace in one pass).

## Expected outcome

Every listed test file passes, with zero regressions in each package's
pre-existing suite.

## Actual outcome

All green: `catalyst-core` 203/203 (189 pre-existing + 14 new),
`catalyst-host-electron` 16/16 (unaffected), `catalyst-host-vscode`
79/79 (unaffected), `catalyst-ui` 25/25 (unaffected) — 323 tests total,
zero regressions. `npx tsc --build --force` clean across every
workspace; `npm run lint` and `npm run format:check` clean.

## Related

`REQ-000012-UVqkd7cL`, `STEP-000005-UVqkd7cL`, `STEP-000006-UVqkd7cL`.
