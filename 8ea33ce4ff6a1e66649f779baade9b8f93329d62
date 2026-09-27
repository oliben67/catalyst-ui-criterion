# `RUNMONITOR` — Live run checklist and ledger

**Document:** rules/catalyst-host-vscode-rules.md
**Name:** live-run-checklist-and-ledger
**Defined:** 2026-09-06
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantee `catalyst-host-vscode` makes for surfacing an
agent's own live run-state: a "Runs" tree section listing every
`RUN-NNNNNN` `catalyst-core` parses, each expandable into its checklist
and ledger, with drift (`⚠️`) visible on the section label as soon as
the watcher picks up the file mutation — before the run itself
completes. Consumes `catalyst-core`'s run-state parsing
(`core-CONTRACT-000003-UVqkd7cL`) and `INSPECTOR`'s existing `TreeDataProvider` —
does not redefine either. Read-only: this domain never creates or
edits a run file, only the external agent does (distinct from
`PROPOSAL`, where the UI itself is the writer).

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for run-state
parsing and `hasDrift`, and on `INSPECTOR` (this document) for the tree
provider this domain's section is added to; does not amend either.
Independent of `PROPOSAL` — both are sibling tree sections fed by
`catalyst-core`, but a run's ledger citing a `PROP-` id is informational
text only, not a structural link between the two domains.
