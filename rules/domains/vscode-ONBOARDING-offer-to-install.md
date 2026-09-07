# `ONBOARDING` — Offer to install catalyst

**Document:** rules/catalyst-host-vscode-rules.md
**Defined:** 2026-09-06
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantee `catalyst-host-vscode` makes when a workspace
folder resolves to no catalyst deployment: rather than the silent
empty state `INSPECTOR` falls back to, this domain makes that state
actionable — offering to copy a ready instantiation prompt to the
clipboard, naming a discovered or configured catalyst framework repo
location. Never performs the instantiation itself: catalyst's own
`BOOTSTRAP.md` is written to be followed by a reasoning coding agent,
not run as a deterministic script, so there is nothing for this
extension to execute on the user's behalf beyond handing off a
well-formed starting prompt.

## Relationship to other domains

Depends on `INSPECTOR` (`rules/catalyst-host-vscode-rules.md`) only for
the fact of a workspace folder having no resolvable deployment (via
`catalyst-core`'s `resolveCorpusRoot` returning `null`) — does not
amend `INSPECTOR`'s own behavior for folders that *do* resolve.
Independent of `PROPOSAL`/`RUNMONITOR`/`HEALTH`: this domain runs
before any of those become relevant, since they all assume a resolved
deployment already exists.
