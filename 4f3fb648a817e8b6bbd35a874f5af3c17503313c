# `ONBOARDING` — Offer to install catalyst

**Document:** rules/catalyst-host-vscode-rules.md
**Name:** offer-to-install-catalyst
**Defined:** 2026-09-06
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantee `catalyst-host-vscode` makes for a workspace
folder that isn't cleanly on a current, supported catalyst deployment —
two distinct cases, both made actionable rather than silently degraded
or ignored:

- **No resolvable deployment** (`vscode-ONBOARDING-000001-UVqkd7cL`):
  offering to copy a ready instantiation prompt to the clipboard,
  naming a discovered or configured catalyst framework repo location.
  Never performs the instantiation itself: catalyst's own
  `BOOTSTRAP.md` is written to be followed by a reasoning coding agent,
  not run as a deterministic script, so there is nothing for this
  extension to execute on the user's behalf beyond handing off a
  well-formed starting prompt.
- **A deployment resolves, but its framework version is behind what
  this extension has verified or requires**
  (`vscode-ONBOARDING-000002-UVqkd7cL`): offering a `/sync-framework`
  action, with stronger wording below `catalyst-core`'s own declared
  minimum. Same posture — never runs anything without the user
  explicitly choosing to.

## Relationship to other domains

Depends on `INSPECTOR` (`rules/catalyst-host-vscode-rules.md`) only for
the fact of a workspace folder having no resolvable deployment (via
`catalyst-core`'s `resolveCorpusRoot` returning `null`) — does not
amend `INSPECTOR`'s own behavior for folders that *do* resolve.
Independent of `PROPOSAL`/`RUNMONITOR`/`HEALTH`: this domain runs
before any of those become relevant, since they all assume a resolved
deployment already exists.
