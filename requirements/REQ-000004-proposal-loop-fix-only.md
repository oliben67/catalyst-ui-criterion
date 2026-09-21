# `REQ-000004-UVqkd7cL` — Proposal loop, fix-only

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000004-UVqkd7cL` |
| **Name** | `proposal-loop-fix-only` |
| **Filename** | `REQ-000004-proposal-loop-fix-only.md` |
| **Status** | done |
| **Opened** | 2026-09-05 |
| **Targets** | `core-CONTRACT-000002-UVqkd7cL`, `vscode-PROPOSAL-000001-UVqkd7cL` |
| **Domain** | `PROPOSAL` |
| **Feature** | `FEAT-000004-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `catalyst-core`'s proposal parsing/tracking
(`core-CONTRACT-000002-UVqkd7cL`) and `catalyst-host-vscode`'s propose-fix Quick Fix
plus pending-badge display (`vscode-PROPOSAL-000001-UVqkd7cL`). The UI's first write
path: it only ever creates a `proposals/PROP-NNNNNN.md` file, never
edits a governed file directly.

## Acceptance

- `catalyst-core` parses `proposals/*.md` into a typed list (id, status,
  intent, targets, expectations, constraints), included in
  `watchCorpus`'s update alongside the model and validation report.
- `nextProposalId` never reuses an id; `openProposalsByTarget` groups
  every non-`applied` proposal by each id it targets.
- A "Propose fix" Quick Fix is offered on any catalyst diagnostic, with
  a default `Expectations` sentence per issue kind, and creates a
  correctly-targeted proposal file.
- The same Quick Fix is *not* offered when an open proposal already
  targets the node (no duplicate open proposals against the same
  target).
- The chain inspector tree and node-detail webview show a pending
  indicator, and the webview lists open proposals, for any node targeted
  by an open proposal.
- No automatic `stale`-timeout detection, and no UI-driven state
  transition — an agent moves a proposal's `Status` forward, the UI only
  displays it.

## Notes

Targets two rules: `core-CONTRACT-000002-UVqkd7cL` (the parsing/tracking is real,
independent core infrastructure future hosts will also need — unlike
Phase 2's corpus-discovery addition, which had no independent meaning of
its own) and `vscode-PROPOSAL-000001-UVqkd7cL` (the VS Code UI built on top of it).
