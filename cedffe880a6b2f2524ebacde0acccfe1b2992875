# catalyst-host-vscode rules

Product behavior rules for `packages/catalyst-host-vscode` — the VS Code
extension adapting `catalyst-core`'s protocol to a sidebar tree and a
node-detail webview, and `packages/catalyst-ui`'s shared React surface
mounted inside that webview. Distinct from `catalyst-core-rules.md`
(prefix `core`), which governs the corpus parser/model/validator/watcher
this domain consumes but does not redefine.

## Contents

- [`INSPECTOR`](#inspector) — `vscode-INSPECTOR-000001-UVqkd7cL`
- [`HEALTH`](#health) — `vscode-HEALTH-000001-UVqkd7cL`
- [`PROPOSAL`](#proposal) — `vscode-PROPOSAL-000001-UVqkd7cL`, `vscode-PROPOSAL-000002-UVqkd7cL`
- [`RUNMONITOR`](#runmonitor) — `vscode-RUNMONITOR-000001-UVqkd7cL`
- [`ONBOARDING`](#onboarding) — `vscode-ONBOARDING-000001-UVqkd7cL`
- [`AGENT`](#agent) — `vscode-AGENT-000001-UVqkd7cL`

## `INSPECTOR`

> **Domain:** `INSPECTOR` — see [domains/vscode-INSPECTOR-chain-tree-and-node-detail-webview.md](domains/vscode-INSPECTOR-chain-tree-and-node-detail-webview.md).

### `vscode-INSPECTOR-000001-UVqkd7cL` Read-only chain tree and node-detail webview

✅ working. The extension resolves a catalyst deployment independently
for every open workspace folder — not just the first, in a multi-root
workspace — from each folder's own `<name>.catalyst` pointer file
(`agent-source` field), watches each resolved corpus independently via
`catalyst-core`'s `watchCorpus`, and reacts live to folders being added
to or removed from the workspace
(`vscode.workspace.onDidChangeWorkspaceFolders`) without requiring a
reload. Exposes a sidebar `TreeDataProvider`: with exactly one resolved
deployment its root shows that deployment's six sections directly
(dev artifacts, rules, rules of rules — rules whose id starts `rr-` —
domains, features, steps; work items excluded — none active in this
deployment) — identical to the original single-folder UX; with more
than one, the root instead shows one collapsible entry per deployment,
named after its workspace folder, each expanding into its own six
sections. A requirement with at least one `STEP-NNNNNN` pointing at it
(resolved via the chain model's reverse edges) becomes expandable,
listing its own steps as children — the only node kind in this tree
with children today. Selecting a node opens a `WebviewPanel` —
`catalyst-ui`'s bundled React surface — showing that node's own fields
plus what it's justified by (upstream) and what it produces
(downstream, which is how a requirement's steps also surface in its own
detail view); the underlying command carries which deployment the node
came from, since node ids are only unique within one corpus. Read-only:
no editing, no live-pushed webview updates (reopening the panel
refreshes it). A folder with no resolvable catalyst deployment is
handled by `vscode-ONBOARDING-000001-UVqkd7cL` instead of staying
silent. Targeted by `REQ-000002-UVqkd7cL`, extended by
`REQ-000008-UVqkd7cL` for multi-root and `REQ-000010-UVqkd7cL` for
steps.

Implemented: `packages/catalyst-core/src/discover.ts` (corpus
resolution) plus `watchCorpus`'s `{ model, report, proposals, runs }`
callback and the `NodeDetailPayload` protocol type;
`packages/catalyst-host-vscode/src/{tree,detail,extension}.ts` (sidebar
tree, webview payload builder, real `activate()`); `packages/
catalyst-ui/src/{NodeDetail.tsx, webview-entry.tsx}` (the mounted React
surface, bundled via `esbuild` into `dist/webview.js`). Multi-root
specifically: `extension.ts`'s `ChainInspectorProvider` keeps a
`Map<corpusRoot, DeploymentView>` instead of one flat set of fields;
`setupDeployment`/`teardownFolder` register and dispose one
`WatcherHandle` plus one `DefinitionProvider`/`CodeLensProvider`/
`CodeActionsProvider` set per resolved folder; `refreshDiagnosticsFor
Deployment` tracks each deployment's own previously-reported files so
one deployment's refresh never clears another's diagnostics (a real
bug caught during design review before it shipped — the original
single-folder code called a global `collection.clear()`, which would
have wiped every other deployment's diagnostics the moment any one
watcher fired). Steps specifically: `ChainInspectorProvider`'s
`hasStepChildren`/`stepChildrenFor` resolve a requirement's own steps
from `model.reverseEdges` — the tree's only parent/child nesting
between two real `ChainNode`s today — rendered through the same generic
`"node"` tree-item shape every other kind already uses, no new
`InspectorTreeItem` variant needed. Tested: `npm run lint`, `npm run
format:check`, `npm run typecheck`, `npm test` (73 tests in this
package, 294 across every workspace) all exit zero;
`extension.ts` itself stays a thin, untested glue layer over the real
`vscode` API, same deliberate deferral as always — no real multi-root
Extension Host was launched this session, so the tree-grouping and
live add/remove behavior is verified by design, typecheck (the
discriminated `InspectorTreeItem` union catches most wiring mistakes at
compile time), and the tested pure pieces it's built from, not an
actual running instance. Known, accepted characteristic (not a bug): a
rule or feature whose own prose says "Targeted by `REQ-X`" creates a
real mutual citation with that requirement's `Targets`/`Feature` field,
so such a node can legitimately appear in both a requirement's upstream
and downstream lists.

## `HEALTH`

> **Domain:** `HEALTH` — see [domains/vscode-HEALTH-diagnostics-definitions-and-codelens.md](domains/vscode-HEALTH-diagnostics-definitions-and-codelens.md).

### `vscode-HEALTH-000001-UVqkd7cL` Diagnostics, click-to-jump, and CodeLens for corpus files

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
proposal loop). Targeted by `REQ-000003-UVqkd7cL`.

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
layer, same deliberate deferral as `vscode-INSPECTOR-000001-UVqkd7cL`. Verified
end-to-end against this deployment's own real corpus: diagnostics
mapping confirmed against both a located issue and a synthetic
id-reuse issue (correctly falling back to `definitionsById`), the
definition provider resolved a real `Targets` citation to its actual
line, and CodeLens produced sensible output for `REQ-000001-UVqkd7cL` and
`core-CONTRACT-000001-UVqkd7cL`'s real files — which is what caught a wording bug:
generic "Targets X / Referenced by Y" read backwards for an edge that
comes from mutual prose citation rather than a structural field (a rule
doesn't "target" a requirement just because its own text says
"Targeted by `REQ-X`"); changed to direction-neutral "Links to / Linked
from" before this was marked done.

## `PROPOSAL`

> **Domain:** `PROPOSAL` — see [domains/vscode-PROPOSAL-fix-and-authoring-proposals.md](domains/vscode-PROPOSAL-fix-and-authoring-proposals.md).

### `vscode-PROPOSAL-000001-UVqkd7cL` Propose-fix code action and pending badges

✅ working. Every catalyst diagnostic (`vscode-HEALTH-000001-UVqkd7cL`)
gets a "Propose fix" Quick Fix (`CodeActionProvider`) that creates a new
`proposals/PROP-NNNNNN.md` targeting the affected node, with a default
`Expectations` sentence per issue kind — refused (no action offered) if
an open, non-`applied` proposal already targets that node. The chain
inspector tree and node-detail webview show a pending indicator, and the
webview lists open proposals, for any node targeted by an open proposal
(`catalyst-core`'s `openProposalsByTarget`). Creating a proposal is the
only write this extension ever performs — governed files (rules,
requirements, ...) are never touched by the UI. Targeted by
`REQ-000004-UVqkd7cL`.

Implemented: `packages/catalyst-host-vscode/src/codeactions.ts`
(`canProposeFix`, `defaultExpectationFor`, `buildProposeFixContent`) and
`src/proposals.ts` (`buildProposalSection`, `renderProposalContent`,
shared with `vscode-PROPOSAL-000002-UVqkd7cL`), wired into `extension.ts`'s
`registerCodeActionsProvider` and the `catalyst.proposeFix` command;
`ChainInspectorProvider` tracks `getPendingTargets`/`getAllProposals`
and renders a `⏳` mark on any pending node plus a "Proposals (N)" tree
section. Tested: `npm run lint`, `npm run format:check`, `npm run
typecheck`, `npm test` (106 tests across all four packages) all exit
zero; `extension.ts` itself stays thin, untested glue, same deliberate
deferral as `vscode-INSPECTOR-000001-UVqkd7cL`/`vscode-HEALTH-000001-UVqkd7cL`.

### `vscode-PROPOSAL-000002-UVqkd7cL` Authoring composer

✅ working. A `catalyst.composeProposal` command gathers
structured intent for a brand-new artifact (type, domain, targets,
title, description) via a multi-step input, then compiles it into a
proposal the same way `vscode-PROPOSAL-000001-UVqkd7cL` does — same file format,
same pending-badge treatment, same "the UI only ever proposes" rule.
Works for any rule-linked artifact type this deployment actually has
(rule, requirement, bug, house-keeping); this deployment has no
project-management plugin active, so it cannot create or verify a work
item specifically. Targeted by `REQ-000005-UVqkd7cL`.

Implemented: `packages/catalyst-host-vscode/src/composer.ts`
(`buildAuthoringProposalContent`, `ComposableArtifactType`), wired into
`extension.ts`'s `catalyst.composeProposal` command (a `showQuickPick` +
`showInputBox` sequence for type/domain/title/description/targets),
reusing `proposals.ts`'s `renderProposalContent` — no second file
format or pending-badge path. Tested: `npm run lint`, `npm run
format:check`, `npm run typecheck`, `npm test` (106 tests) all exit
zero; verified end-to-end via a scratchpad script generating a real
proposal against this deployment's own corpus (a "Compose: Sample new
rule" proposal targeting `core-CONTRACT-000001-UVqkd7cL`) confirming the rendered
content matches `renderProposalContent`'s field-table/section format.

## `RUNMONITOR`

> **Domain:** `RUNMONITOR` — see [domains/vscode-RUNMONITOR-live-checklist-and-ledger.md](domains/vscode-RUNMONITOR-live-checklist-and-ledger.md).

### `vscode-RUNMONITOR-000001-UVqkd7cL` Live run checklist and ledger

✅ working. The chain inspector tree gets a "Runs (N)"
section, sibling to the existing proposals section, listing every
`RUN-NNNNNN` `catalyst-core` parses (`core-CONTRACT-000003-UVqkd7cL`): each run
expands to its checklist (one line per step, glyph rendered per its
parsed status) and ledger. The section's own label carries a `⚠️`
suffix whenever any run has drift (`hasDrift`), and any run currently
`running` is visually distinguishable from `completed`/`failed` — this
is what makes a drift event visible while the run is still in
progress, not just after. Read-only, same as every other tree section:
the extension never creates or edits a run file, only the external
agent does. Targeted by `REQ-000007-UVqkd7cL`.

Implemented: `packages/catalyst-host-vscode/src/runmonitor.ts`
(`buildRunSection`, `formatRunLabel`, `formatStepLabel`), wired into
`extension.ts`'s `ChainInspectorProvider` as a new `run-section`/`run`/
`run-step`/`run-ledger-entry` tree-item family, fed by `watchCorpus`'s
new `runs` field. Tested: `npm run lint`, `npm run format:check`, `npm
run typecheck`, `npm test` (119 tests total, 10 new in
`runmonitor.test.ts`) all exit zero; `extension.ts` itself stays thin,
untested glue, same deliberate deferral as every other domain in this
document. Verified end-to-end: a simulated agent-authored `RUN-000001`
file with a `⚠️` checklist line produced section label `Runs (1) ⚠️`
and run label `RUN-000001 — running ⚠️` while the run's own `Status`
was still `running` — the concrete form of "a drift event is visible
in the UI before the run completes," this deployment's own roadmap
exit criterion.

## `ONBOARDING`

> **Domain:** `ONBOARDING` — see [domains/vscode-ONBOARDING-offer-to-install.md](domains/vscode-ONBOARDING-offer-to-install.md).

### `vscode-ONBOARDING-000001-UVqkd7cL` Offer to install catalyst when no deployment is found

✅ working. When a workspace folder has no resolvable
`*.catalyst` pointer, the extension offers to help rather than staying
silent: an information message with an "Install catalyst…" action (and
a "Don't ask again" dismissal, remembered per folder). Since catalyst's
own instantiation is an agent-driven procedure (`BOOTSTRAP.md` is
written to be followed by a reasoning coding agent, not run as a
deterministic script — per catalyst's own framework repository), this
extension cannot perform the install itself; it copies a ready
instantiation prompt to the clipboard instead, naming the framework
repo location (auto-detected as a sibling directory containing
`BOOTSTRAP.md`, else the `catalyst.frameworkPath` setting) and this
project's own root, then tells the user to paste it into whichever
coding agent they use. Never auto-runs anything — no CLI, extension,
or agent is assumed to be installed. Targeted by `REQ-000008-UVqkd7cL`.

Implemented: `packages/catalyst-host-vscode/src/framework-discovery.ts`
(`findSiblingFrameworkRepo`, `buildInstantiationPrompt` — pure, no
`vscode` import, fully tested), `extension.ts`'s `offerToInstall`
(the `showInformationMessage`/`showWarningMessage`/clipboard glue,
dismissal tracked in `context.workspaceState`) and new `contributes.
configuration` entry `catalyst.frameworkPath`. Tested: `npm run lint`,
`npm run format:check`, `npm run typecheck`, `npm test` (124 tests
total, 5 new in `framework-discovery.test.ts`: sibling found/not-found/
ignores-itself/missing-parent, and the prompt's shape) all exit zero.
Verified end-to-end against this machine's own real directory layout
(not a fixture): `findSiblingFrameworkRepo` run against `catalyst-ui`'s
real project root correctly found the real `catalyst` framework
checkout cloned beside it and produced a well-formed instantiation
prompt naming both real paths.

## `AGENT`

> **Domain:** `AGENT` — see [domains/vscode-AGENT-run-slash-commands.md](domains/vscode-AGENT-run-slash-commands.md).

### `vscode-AGENT-000001-UVqkd7cL` Run catalyst slash commands via a per-project agent terminal

❌ not yet implemented. A `catalyst.runSlashCommand` command discovers
the deployed `.claude/commands/*.md` slash commands for a workspace
folder (`catalyst-core`'s `discoverSlashCommands`), lets the user pick
which project (when more than one is open) and which command, prompts
for arguments when the command declares an `argument-hint`, then sends
the composed line (`composeSlashCommand`) to a `vscode.window.Terminal`
running that project's own agent CLI (`resolveAgentCommand`, read from
the `*.catalyst` pointer's `agent` field). One terminal per resolved
folder, not a single shared one — reusing a stale terminal would send
a different project's command into whatever agent process happens to
still be running in it. The terminal is branded (the extension's own
icon, named after the project, `cwd` set to the project root) and
opens in the editor area beside the current view — the same surface
`vscode-INSPECTOR-000001-UVqkd7cL`'s node-detail webview uses — rather than the
generic bottom Terminal panel shared by every other tool. Targeted by
`REQ-000009-UVqkd7cL`.

## Known Bugs — Quick Index

*(none yet — no implementation exists to have found bugs in)*
