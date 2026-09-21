# `REQ-000005-UVqkd7cL` — Authoring composer

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000005-UVqkd7cL` |
| **Name** | `authoring-composer` |
| **Filename** | `REQ-000005-authoring-composer.md` |
| **Status** | done |
| **Opened** | 2026-09-05 |
| **Targets** | `vscode-PROPOSAL-000002-UVqkd7cL` |
| **Domain** | `PROPOSAL` |
| **Feature** | `FEAT-000005-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

A `catalyst.composeProposal` command gathering structured intent for a
new artifact (type, domain, targets, title, description), compiled into
a proposal via `REQ-000004-UVqkd7cL`'s same mechanism — no second write path.

## Acceptance

- The command produces a well-formed proposal for a new rule,
  requirement, bug, or house-keeping artifact (whichever this deployment
  actually supports).
- The generated `Expectations` say the new artifact has a valid,
  never-reused id and resolves all links on first parse (the roadmap's
  own exit-criterion wording, generalized beyond "work item" since none
  are active here).
- Same pending-badge and duplicate-target refusal behavior as
  `REQ-000004-UVqkd7cL`'s proposals — no separate rules for this.
- Explicitly does not claim to create or verify a *work item* — no
  project-management plugin is active in this deployment, so that
  specific path cannot be exercised or verified here.

## Notes

Builds on `REQ-000004-UVqkd7cL`'s proposal mechanism; targets only
`vscode-PROPOSAL-000002-UVqkd7cL` since it's the same underlying write path with a
different entry point, not new core infrastructure.
