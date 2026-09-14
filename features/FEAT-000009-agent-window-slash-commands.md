# `FEAT-000009` — Agent window for running catalyst slash commands

A feature entry documents a new or future piece of functionality for the
app — an idea, a roadmap item, a product direction. It is **not** a
rule-linked, measured artifact. Once work on a feature actually starts,
open a `REQ-NNNNNN` requirement that targets or proposes the rule(s) the
feature requires — see `Requirement(s)` below.

| Field | Value |
|---|---|
| **ID** | `FEAT-000009` |
| **Filename** | `FEAT-000009-agent-window-slash-commands.md` |
| **Status** | in-development |
| **Opened** | 2026-09-08 |
| **Area** | catalyst-core, catalyst-host-vscode, catalyst-host-electron |
| **Roadmap** | `RM-000009` |
| **Requirement(s)** | `REQ-000009` |
| **Signed-off-by** | Olivier Steck |

## Description

Run a deployed `.claude/commands/*.md` slash command straight through
the deployment's own agent CLI from inside either host's UI, instead
of a manual copy-paste into an unrelated terminal — landing in a
per-project agent window/terminal that's part of the extension/app,
not a shared one that can cross-send a command into the wrong
project's live session.

## Motivation

The VS Code half of this was already built directly (not through this
governance process) while other work was in flight; formalizing it now
also caught and fixes a real bug in it (a single shared terminal across
every open project) and brings the equivalent capability to the
Electron app, which had none.

## Rough scope

In: three shared helpers promoted into `catalyst-core`
(`resolveAgentCommand`, `discoverSlashCommands`, `composeSlashCommand`);
`catalyst-host-vscode`'s per-folder branded terminal fix; a brand-new
agent window in `catalyst-host-electron` (spawned process, piped
output, follow-up input — not a real pty, no new native dependency).
Out: a real pty/xterm.js terminal for Electron (a deliberate,
dependency-cost trade-off, not a gap); anything that runs a command
without the user picking it first (no automatic/triggered command
runs).

## Open questions

None specific to this feature.

## Related

`REQ-000009` implements this feature.
