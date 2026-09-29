# `FEAT-000005-UVqkd7cL` — Authoring composer

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000005-UVqkd7cL` |
| **Name** | `authoring-composer` |
| **Filename** | `FEAT-000005-authoring-composer.md` |
| **Status** | Completed |
| **Opened** | 2026-09-05 |
| **Area** | catalyst-host-vscode |
| **Roadmap** | `RM-000005-UVqkd7cL` |
| **Requirement(s)** | `REQ-000005-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

A command that gathers structured intent for a brand-new artifact
(type, domain, targets, title, description) and compiles it into a
proposal via the same mechanism Phase 4 built, instead of a hand-typed
one-line intent. Same loop, harder expectations: creating something new
with a valid, never-reused id, rather than fixing something that already
exists.

## Motivation

Reuses Phase 4's proposal mechanism rather than building a second write
path, proving the same loop generalizes beyond "fix an existing thing."

## Rough scope

In: a multi-step input command producing a well-formed proposal for a
new rule/requirement/bug/house-keeping artifact. Out: this deployment
has no project-management plugin active, so there is no *work item* to
create — the roadmap's own exit criterion names one, and this deployment
cannot literally exercise that path. Verified instead against a rule or
requirement, called out plainly rather than claimed as satisfied.

## Open questions

- None specific to this phase, beyond the work-items gap noted above.

## Related

`REQ-000005-UVqkd7cL` implements this feature. Builds on `FEAT-000004-UVqkd7cL`'s proposal
mechanism.
