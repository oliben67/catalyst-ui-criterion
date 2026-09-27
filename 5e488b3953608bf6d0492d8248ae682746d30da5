# `PROP-NNNNNN` — short title

> Copy this file to `proposals/templates/TEMPLATE-PROPOSAL-v1.md` and resolve every `{{PLACEHOLDER}}` (INV-20). See `INSTANTIATION-GUIDE.md`.

A proposal is a reviewable, agent-mediated write request — the only path
from the read-only chain inspector/health board to an actual change on a
governed file. The UI that creates one never edits governed files
itself; an agent (a human-directed Claude Code session, or another
agent) reads the proposal separately and performs the real edit,
updating this file's own `Status` as it works. Permanent, never-reused
ID — same scheme as every other artifact type.

| Field | Value |
|---|---|
| **ID** | `PROP-NNNNNN` |
| **Filename** | descriptive kebab-case filename, e.g. `PROP-000001-fix-orphaned-req.md` |
| **Status** | proposed / applying / applied / partial / stale |
| **Opened** | YYYY-MM-DD |
| **Signed-off-by** | name of the registered user (`IAM/users/users.json`) who signed this entry — see `CODE-OF-CONDUCT.md` §2 |

## Intent

One-line human statement of what and why — this is the prompt the agent
reads.

## Targets

Existing node IDs this proposal touches, one per line, each as a
backtick-quoted id (e.g. `` `REQ-000001` ``). The UI refuses to open a
second proposal against any id already targeted by an open (non-
`applied`) proposal.

## Expectations

Checkable post-conditions, one per line, that must hold after the agent
acts and the corpus reparses (e.g. "`REQ-000001` has a non-empty
`Targets` field"). Executing/checking these is the agent's job, not
this deployment's validator.

## Constraints

Invariants or rules to re-read before acting, by path — points at the
relevant document, does not restate it (e.g. "`CODE-OF-CONDUCT.md` §1").

## Reconciliation

Filled in by whoever applies this proposal, not at creation time.

- **Resolved**: YYYY-MM-DD, once no longer `proposed`
- **Outcome**: what happened — required for `partial`/`stale`, explaining which expectations weren't met or why nothing changed
