# catalyst-host-vscode rules

Product behavior rules for `packages/catalyst-host-vscode` — the VS Code
extension adapting `catalyst-core`'s protocol to a sidebar tree and a
node-detail webview, and `packages/catalyst-ui`'s shared React surface
mounted inside that webview. Distinct from `catalyst-core-rules.md`
(prefix `core`), which governs the corpus parser/model/validator/watcher
this domain consumes but does not redefine.

## Contents

- [`INSPECTOR`](#inspector) — `vscode-INSPECTOR-001`
- [`HEALTH`](#health) — `vscode-HEALTH-001`

## `INSPECTOR`

> **Domain:** `INSPECTOR` — see [domains/vscode-INSPECTOR-chain-tree-and-node-detail-webview.md](domains/vscode-INSPECTOR-chain-tree-and-node-detail-webview.md).

### `vscode-INSPECTOR-001` Read-only chain tree and node-detail webview

✅ working. The extension resolves which catalyst deployment to inspect
from the opened project's own `<name>.catalyst` pointer file
(`agent-source` field), watches it via `catalyst-core`'s `watchCorpus`,
and exposes a sidebar `TreeDataProvider` grouping the chain model's nodes
by layer: dev artifacts, rules, rules of rules (rules whose id starts
`rr-`), domains, features (work items excluded — none active in this
deployment). Selecting a node opens a `WebviewPanel` — `catalyst-ui`'s
bundled React surface — showing that node's own fields plus what it's
justified by (upstream, via the chain model's resolved edges) and what
it produces (downstream, via reverse edges). Read-only: no editing, no
live-pushed webview updates (reopening the panel refreshes it). No
catalyst deployment found for the opened project is a graceful empty
state, not an error. Targeted by `REQ-000002`.

Implemented: `packages/catalyst-core/src/discover.ts` (corpus
resolution) plus `watchCorpus`'s extended `{ model, report }` callback
and the `NodeDetailPayload` protocol type; `packages/catalyst-host-
vscode/src/{tree,detail,extension}.ts` (sidebar tree, webview payload
builder, real `activate()`); `packages/catalyst-ui/src/{NodeDetail.tsx,
webview-entry.tsx}` (the mounted React surface, bundled via `esbuild`
into `dist/webview.js`). Tested: `npm run lint`, `npm run format:check`,
`npm run typecheck`, `npm test` (56 tests: Vitest for catalyst-core/
catalyst-ui, Mocha for catalyst-host-vscode's `tree.ts`/`detail.ts`)
all exit zero. `extension.ts` itself stays a thin, untested glue layer
over the real `vscode` API — full `@vscode/test-electron` integration
testing is deliberately deferred, the devDependency stays in place.
Verified end-to-end against this deployment's own real corpus (not just
fixtures): 40 nodes resolved and correctly grouped into all five
sections; a real bug this caught and fixed — a node's own backtick-quoted
`**ID**` field was read back as a self-reference, creating a self-loop
in the chain model — is covered by a regression test in `catalyst-core`.
Known, accepted characteristic (not a bug): a rule or feature whose own
prose says "Targeted by `REQ-X`" creates a real mutual citation with
that requirement's `Targets`/`Feature` field, so such a node can
legitimately appear in both a requirement's upstream and downstream
lists — already true of Phase 1's docs, just newly visible now that a
node's neighbors are actually rendered.

## `HEALTH`

> **Domain:** `HEALTH` — see [domains/vscode-HEALTH-diagnostics-definitions-and-codelens.md](domains/vscode-HEALTH-diagnostics-definitions-and-codelens.md).

### `vscode-HEALTH-001` Diagnostics, click-to-jump, and CodeLens for corpus files

✅ working. The validation report is surfaced as native VS Code
diagnostics (`DiagnosticCollection`, refreshed on every watcher
update) against each issue's `location` — this gives a native worklist
(the Problems panel), click-to-jump, and gutter marks all from one API.
Any backtick-quoted id in a corpus markdown file is a jump target (a
`DefinitionProvider` resolving the token under the cursor via the chain
model's nodes). Each node's own heading/field-table gets a CodeLens
summarizing what it links to/from, opening that node's detail via the
existing `catalyst.showNodeDetail` command. All three are scoped to the
resolved corpus root's markdown files only. Still read-only — no
"propose fix" actions (Phase 4) or drift/pending badges (need the
proposal loop). Targeted by `REQ-000003`.

Implemented: `packages/catalyst-host-vscode/src/{diagnostics,
definitions,codelens}.ts` (pure, vscode-free logic) wired into
`extension.ts` via `vscode.languages.createDiagnosticCollection`,
`registerDefinitionProvider`, and `registerCodeLensProvider`. Also
exported `BACKTICK_RULE_ID_RE`/`BACKTICK_DEV_ARTIFACT_ID_RE`/
`BACKTICK_FEATURE_ID_RE` from `catalyst-core`'s `index.ts` (existed
internally already, just not public) so the definition provider reuses
them instead of re-deriving what counts as an id. Tested: `npm run
lint`, `npm run format:check`, `npm run typecheck`, `npm test` (67
tests) all exit zero; `extension.ts` itself stays a thin, untested glue
layer, same deliberate deferral as `vscode-INSPECTOR-001`. Verified
end-to-end against this deployment's own real corpus: diagnostics
mapping confirmed against both a located issue and a synthetic
id-reuse issue (correctly falling back to `definitionsById`), the
definition provider resolved a real `Targets` citation to its actual
line, and CodeLens produced sensible output for `REQ-000001` and
`core-CONTRACT-001`'s real files — which is what caught a wording bug:
generic "Targets X / Referenced by Y" read backwards for an edge that
comes from mutual prose citation rather than a structural field (a rule
doesn't "target" a requirement just because its own text says
"Targeted by `REQ-X`"); changed to direction-neutral "Links to / Linked
from" before this was marked done.

## Known Bugs — Quick Index

*(none yet — no implementation exists to have found bugs in)*
