# `STEP-000001-UVqkd7cL` — Parse and validate steps in catalyst-core

| Field | Value |
|---|---|
| **ID** | `STEP-000001-UVqkd7cL` |
| **Name** | `parse-and-validate-steps-in-catalyst-core` |
| **Filename** | `STEP-000001-parse-and-validate-steps-in-catalyst-core.md` |
| **Requirement** | `REQ-000010-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-09-19 |
| **Closed** | 2026-09-19 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Give `catalyst-core` a typed `StepNode`, teach the parser to read
`steps/`, and wire the `Requirement` cross-reference into the graph and
validator — the data-model half of `REQ-000010-UVqkd7cL`.

## Actions performed

- `packages/catalyst-core/src/types.ts`: added `"step"` to `NodeKind`,
  `StepStatus`, and `StepNode extends ChainNodeBase` (`requirement`,
  `status`, `signedOffBy?`, `registered`, `fileExists`, `description`,
  `content`); added `StepNode` to the `ChainNode` union.
- `packages/catalyst-core/src/ids.ts`: added `STEP_ID_PATTERN`/
  `STEP_ID_RE`/`BACKTICK_STEP_ID_RE`, registered the backtick regex in
  `collectIdReferences`.
- `packages/catalyst-core/src/parser.ts`: added `buildStepNode`/
  `parseStepCollection`, modeled on `parseFeatureCollection` (own
  index+dir, not rule-linked) rather than the no-index PROP-/RUN-
  pattern, since `steps/steps.md` has a real index table; wired into
  `parseCorpus` as a parallel block to `features/`.
- `packages/catalyst-core/src/graph.ts`: added the
  `node.kind === "step" && node.requirement` edge-building block,
  mirroring the existing `dev-artifact`/`roadmap` blocks.
- `packages/catalyst-core/src/validator.ts`: added a step-specific
  `orphaned-artifact` check (missing `Requirement` field, or a
  registered/fileExists mismatch) — the generic `dangling-reference`
  check already catches an unresolvable `Requirement` id with no new
  code, since a step's `Requirement` field is backtick-quoted and
  already matched by the existing dev-artifact id regex.
- `packages/catalyst-core/src/test/test-support.ts`: added
  `FixtureStep`/`renderStepFile`, wired a `steps?` field into
  `FixtureSpec` and `createFixtureCorpus`.
- Added test coverage: 3 cases in `parser.test.ts` (parse+link, index-only
  ghost, unregistered-file), 1 in `graph.test.ts` (edge resolution), 5 in
  `validator.test.ts` (missing Requirement, registered/fileExists
  mismatches, dangling reference, clean pass).

## Verification

`npx tsc --build --force` clean; `npx vitest run` in
`packages/catalyst-core`: 181/181 passing (172 pre-existing + 9 new,
zero regressions).

## Related

`STEP-000002-UVqkd7cL` (the display half, in `catalyst-host-vscode`/
`catalyst-ui`).
