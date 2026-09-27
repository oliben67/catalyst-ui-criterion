# `DESKTOP` — Multi-project desktop host and graph view

**Document:** rules/catalyst-host-electron-rules.md
**Defined:** 2026-09-05
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantees `catalyst-host-electron` makes: tracking more
than one project's corpus at once, keeping a persistent `watchCorpus`
instance running per tracked project, and a graph view rendering the
chain model's nodes and edges — the one surface the roadmap explicitly
withheld from the VS Code host until this phase. Mounts `catalyst-ui`'s
shared React surface (`NodeDetail`) unchanged, the same way
`catalyst-host-vscode`'s `INSPECTOR` domain does, for the selected
node's detail.

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for the chain
model, validation, and the corpus watcher this domain runs one instance
of per tracked project. Does not depend on or amend `INSPECTOR`,
`HEALTH`, or `PROPOSAL` (`rules/catalyst-host-vscode-rules.md`) — those
govern the VS Code host specifically; this domain is
`catalyst-host-electron`'s own equivalent surface, not an extension of
the VS Code one. Reuses `catalyst-ui`'s `NodeDetail` component as a
plain dependency, without amending `catalyst-ui` itself (Phase 6's own
exit criterion: shipped with no changes to `catalyst-ui`).
