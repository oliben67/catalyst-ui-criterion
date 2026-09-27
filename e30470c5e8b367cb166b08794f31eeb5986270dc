# catalyst-core rules

Product behavior rules for `packages/catalyst-core` — the parser, typed
chain model, global validator, and file watcher every other package
(the two hosts, `catalyst-ui`) consumes through its message protocol.
Distinct from `dev-environment-rules.md` (prefix `env`), which governs
tooling/process, not product behavior — greenfield instantiation's
tooling layer never substitutes for this
(`development-framework/INSTANTIATION-GUIDE.md` §3 step 5, catalyst
repository).

## Contents

- [`CONTRACT`](#contract) — `core-CONTRACT-001`, `core-CONTRACT-002`, `core-CONTRACT-003`

## `CONTRACT`

> **Domain:** `CONTRACT` — see [domains/core-CONTRACT-parser-model-validator-watcher.md](domains/core-CONTRACT-parser-model-validator-watcher.md).

### `core-CONTRACT-001` Typed chain model, global validation, watched changes

✅ working. `catalyst-core` exposes a single message protocol (defined
once, before any host exists) covering: (1) a typed chain model
connecting dev artifacts → rules → rules of rules, built from a full
reparse of the corpus (work items excluded — no project-management
plugin is active in this deployment, so `work-items/` doesn't exist);
(2) global validation that runs on every reparse, never incrementally —
orphaned artifacts, rules without meta-rule backing, ID reuse, and
dangling references are inherently cross-cutting checks, not per-file
ones; (3) a file watcher that debounces/coalesces changes in a
150–200ms trailing window and uses single-flight cancellation, so a
change landing mid-parse aborts and restarts rather than queuing.
Targeted by `REQ-000001`.

Implemented: `packages/catalyst-core/src/{types,ids,parser,graph,validator,watcher,cli,index}.ts`,
tests under `src/test/`. Protocol types (`ChainNode`, `ChainModel`,
`ValidationReport`, ...) published from `index.ts`. Ships as a CLI —
`catalyst-core <corpusRoot> [--watch] [--json]` — printing the
validation report and exiting non-zero on error-severity issues.
Tested: `npm run lint`, `npm run typecheck`, `npm test` (41 tests) all
exit zero; the built CLI run against this deployment's own real corpus
reports 36 nodes, 0 errors; a synthetic 5× corpus (250 rules/domains/
requirements) parses, models, and validates in under 100ms (roadmap
Phase 1's own exit criterion).

### `core-CONTRACT-002` Proposal parsing and reconciliation-state tracking

✅ working. `catalyst-core` parses `proposals/*.md`
(`PROP-NNNNNN`, this deployment's own uniform-layout artifact type —
not a catalyst framework-wide concept) into a `Proposal` list: id,
reconciliation `status` (`proposed` / `applying` / `applied` / `partial`
/ `stale`), `intent`, `targets` (existing node ids), `expectations`, and
`constraints`. Exposes `nextProposalId` (never-reused, same 6-digit
scheme as every other artifact type) and `openProposalsByTarget`
(every non-`applied` proposal grouped by each id it targets, for
pending-state lookups). `catalyst-core` only parses and tracks —
executing a proposal's expectations, and advancing its `status`, is an
agent's job, never this package's or any host's. Included in
`watchCorpus`'s `WatchUpdate` alongside the chain model and validation
report, so proposal state refreshes the same way everything else does.
Targeted by `REQ-000004`.

Implemented: `packages/catalyst-core/src/proposals.ts` (`parseProposals`,
`nextProposalId`, `openProposalsByTarget`), wired into `watcher.ts`'s
`WatchUpdate`. Tested: `npm run lint`, `npm run format:check`, `npm run
typecheck`, `npm test` (56 tests: `proposals.test.ts` plus a
`proposal-loop.integration.test.ts` that seeds a real, validator-detected
orphan and confirms a proposal targeting it is discoverable as open,
then stops being flagged once its only proposal is `applied`) all exit
zero. Verified end-to-end against this deployment's own real corpus:
`parseProposals` resolves the real `proposals/` directory (currently
holding no `PROP-` files yet — README/index/templates only — correctly
returning an empty list rather than erroring), and `nextProposalId`
correctly returns `PROP-000001` for that empty state.

### `core-CONTRACT-003` Run-state parsing

✅ working. `catalyst-core` parses `runs/*.md`
(`RUN-NNNNNN`, this deployment's own uniform-layout artifact type —
not a catalyst framework-wide concept, and unlike `proposals/`, never
created or edited by any host, only by the external agent running a
task) into a `Run` list: id, `status` (`running` / `completed` /
`failed`), `command`, `started`, a `steps` checklist (each a glyph-
parsed `status` — `done` / `failed` / `pending` / `drift` — plus its
text), and a free-text `ledger`. Exposes `hasDrift(run)` — `true` iff
any step's status is `drift` — kept in `catalyst-core` rather than a
host, same reasoning as `openProposalsByTarget`: any future host wants
the identical definition. `catalyst-core` only parses; it never
independently verifies a step's `drift` claim, the same way it never
executes a proposal's `expectations`. Included in `watchCorpus`'s
`WatchUpdate` alongside the chain model, validation report, and
proposals, so a run's live edits refresh the same way everything else
does. Targeted by `REQ-000007`.

Implemented: `packages/catalyst-core/src/runs.ts` (`parseRuns`,
`hasDrift`), `parser.ts`'s `sectionLines`/`bulletItems` promoted from
`proposals.ts`-private to exported so both parsers share them, wired
into `watcher.ts`'s `WatchUpdate`. Tested: `npm run lint`, `npm run
format:check`, `npm run typecheck`, `npm test` (119 tests total, 7 new
in `runs.test.ts`: empty `runs/`, a well-formed run's fields/checklist/
ledger, an unrecognized checklist-line prefix skipped without throwing,
an unrecognized `Status` value defaulting to `running`, sort-by-id, and
`hasDrift` true/false) all exit zero. Verified end-to-end: against this
deployment's own real corpus, `parseRuns` resolves the real (currently
empty) `runs/` directory without error; a simulated agent-authored
`RUN-000001` file (matching `templates/TEMPLATE-RUN-v1.md`'s shape,
with a `⚠️` checklist line) parsed correctly into a `drift`-status step,
and `hasDrift` correctly returned `true` while the run's own `Status`
was still `running` — the concrete proof that a drift event is
detectable before a run completes.

## Known Bugs — Quick Index

*(none yet — no implementation exists to have found bugs in)*
