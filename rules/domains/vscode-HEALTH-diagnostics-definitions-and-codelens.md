# `HEALTH` — Health board and editor affordances contract

**Document:** rules/catalyst-host-vscode-rules.md
**Name:** health-board-and-editor-affordances-contract
**Defined:** 2026-09-05
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantees `catalyst-host-vscode` makes for the read-only
health board and editor affordances: the validation report surfaced as
native VS Code diagnostics, click-to-jump navigation on any cited id, and
CodeLens summarizing a node's own resolved links. Consumes `catalyst-
core`'s validation report and chain model (`core-CONTRACT-000001-UVqkd7cL`) and
`INSPECTOR`'s node-detail command — does not redefine either.

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for the
validation report and chain model, and on `INSPECTOR` (this document)
for the `catalyst.showNodeDetail` command CodeLens clicks open; does not
amend either.
