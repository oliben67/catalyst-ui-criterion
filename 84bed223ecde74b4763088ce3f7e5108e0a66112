# `AGENT` — Run slash commands via a per-project agent terminal

**Document:** rules/catalyst-host-vscode-rules.md
**Defined:** 2026-09-08
**Parent:** none
**Sub-domains:** none

Rules in this domain do not supersede, amend, or contradict any rule in
another domain unless explicitly stated below against that rule's ID.

## Scope

The behavioral guarantee `catalyst-host-vscode` makes for running a
deployed `.claude/commands/*.md` slash command through the project's
own agent CLI: discovering available commands, composing the picked
one with its arguments, and sending it to a per-project `vscode.
window.Terminal` branded as part of this extension rather than a
generic one. Consumes `catalyst-core`'s `resolveAgentCommand`/
`discoverSlashCommands`/`composeSlashCommand` (`core-CONTRACT-004`) —
does not redefine any of the three.

## Relationship to other domains

Depends on `CONTRACT` (`rules/catalyst-core-rules.md`) for command
discovery and composition. Independent of `INSPECTOR`/`HEALTH`/
`PROPOSAL`/`RUNMONITOR`/`ONBOARDING`: this domain's terminal is a
separate surface from the tree/webview/diagnostics those cover, though
it shares the same per-folder resolution `INSPECTOR` already performs
(a workspace folder must resolve to a deployment before there's
anything to discover commands for).
