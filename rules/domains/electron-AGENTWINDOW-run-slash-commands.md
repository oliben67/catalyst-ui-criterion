# `AGENTWINDOW` — Run slash commands via a per-project agent window

**Document:** rules/catalyst-host-electron-rules.md
**Defined:** 2026-09-08
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantee `catalyst-host-electron` makes for running a
deployed `.claude/commands/*.md` slash command through the project's
own agent CLI: discovering available commands for the selected tracked
project, composing the picked one with its arguments, and sending it
to a spawned agent process — not a real pty, a piped-output panel with
a follow-up input box. Consumes `catalyst-core`'s `resolveAgentCommand`/
`discoverSlashCommands`/`composeSlashCommand` (`core-CONTRACT-004`) —
does not redefine any of the three. Named distinctly from
`catalyst-host-vscode-rules.md`'s own `AGENT` domain (same underlying
core infrastructure, two independent host-specific surfaces, siblings
per this document's own header — neither amends the other).

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for command
discovery and composition, and on `DESKTOP` (this document) only for
the fact of a tracked project already existing — does not amend
`DESKTOP`'s own tracked-project/graph-view behavior.
