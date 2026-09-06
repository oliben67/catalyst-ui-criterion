# `PROPOSAL` — Propose-fix and authoring-composer contract

**Document:** rules/catalyst-host-vscode-rules.md
**Defined:** 2026-09-05
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantees `catalyst-host-vscode` makes for catalyst-ui's
first write path: creating a proposal (never editing a governed file
directly) from a health-board diagnostic (fix-only) or from structured
authoring intent (a new artifact), and displaying pending state on any
node an open proposal targets. Consumes `catalyst-core`'s proposal
parsing (`core-CONTRACT-002`) and `INSPECTOR`'s node-detail command and
chain model — does not redefine either.

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for proposal
parsing/tracking, and on `INSPECTOR` (this document) for the chain model
and node-detail command this domain's rules build on; does not amend
either.
