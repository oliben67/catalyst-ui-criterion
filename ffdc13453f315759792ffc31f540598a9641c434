# `STEP-000005-UVqkd7cL` — Declare and check a minimum framework version in catalyst-core

| Field | Value |
|---|---|
| **ID** | `STEP-000005-UVqkd7cL` |
| **Name** | `declare-and-check-a-minimum-framework-version-in-catalyst-core` |
| **Filename** | `STEP-000005-declare-and-check-a-minimum-framework-version-in-catalyst-core.md` |
| **Parent** | `REQ-000012-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-09-20 |
| **Closed** | 2026-09-20 |
| **Tests** | `TEST-000002-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Give `catalyst-core` a real, declared floor for the framework version
it can correctly parse, expressed as a version specifier rather than a
bare number — the data-model half of `REQ-000012-UVqkd7cL`, the same
split `STEP-000003-UVqkd7cL` used for `TEST-` parsing.

## Actions performed

- `packages/catalyst-core/src/versioning.ts`: added
  `parseVersionSpecifier` (parses one `>=`/`<=`/`==`/`!=`/`>`/`<` clause
  into `{operator, version}`, longer operators checked first so `>=`
  isn't mistaken for `>`, throws on malformed input) and
  `satisfiesVersionSpecifier` (evaluates a version against a specifier
  string via the existing `compareVersions`).
- `packages/catalyst-core/src/discover.ts`: added
  `REQUIRED_FRAMEWORK_VERSION = ">=0.31.0"` (the newest framework
  version this build's parser/graph/validator logic was actually
  verified against) and `meetsRequiredFrameworkVersion`, which treats a
  `null` deployed version (unreadable `version.txt`) as satisfying the
  requirement rather than a false failure.
- `packages/catalyst-core/src/index.ts`: exported the new symbols.
- Added test coverage: `packages/catalyst-core/src/test/versioning.test.ts`
  (every operator, whitespace tolerance, malformed-input errors) and
  `discover.test.ts` (`meetsRequiredFrameworkVersion` at/above/below the
  floor, `null` treated as satisfying it).

## Verification

`npx tsc --build --force` clean; `npx vitest run` in
`packages/catalyst-core`: 203/203 passing (189 pre-existing + 14 new,
zero regressions).

## Related

`STEP-000006-UVqkd7cL` (the enforcement/UI half, in
`catalyst-host-vscode`).
