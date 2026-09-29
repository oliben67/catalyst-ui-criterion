# `REQ-000009-UVqkd7cL` — Agent window for running catalyst slash commands

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000009-UVqkd7cL` |
| **Name** | `agent-window-slash-commands` |
| **Filename** | `REQ-000009-agent-window-slash-commands.md` |
| **Status** | Active |
| **Opened** | 2026-09-08 |
| **Targets** | `core-CONTRACT-000004-UVqkd7cL`, `vscode-AGENT-000001-UVqkd7cL`, `electron-AGENTWINDOW-000001-UVqkd7cL` |
| **Domain** | `AGENT` |
| **Feature** | `FEAT-000009-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Promote `resolveAgentCommand`/`discoverSlashCommands`/
`composeSlashCommand` into `catalyst-core` (`core-CONTRACT-000004-UVqkd7cL`); fix
`catalyst-host-vscode`'s slash-command terminal to be per-project and
branded as part of the extension (`vscode-AGENT-000001-UVqkd7cL`); add the
equivalent capability to `catalyst-host-electron`, which had none
(`electron-AGENTWINDOW-000001-UVqkd7cL`).

## Acceptance

- The three helpers live in `catalyst-core`, exported from `index.ts`,
  with tests converted to Vitest; `catalyst-host-vscode`'s own copies
  and tests are removed, importing from `catalyst-core` instead.
- Running a slash command against project A, then later against
  project B, never sends B's composed command into a terminal/process
  still running A's agent — one per project in both hosts.
- The VS Code terminal is branded (extension icon, named after the
  project, correct `cwd`) and opens beside the current editor view,
  not the generic bottom Terminal panel.
- The Electron app can discover a selected project's slash commands,
  compose one with arguments, run it in a spawned agent process, see
  its piped `stdout`/`stderr`, and send follow-up free-text input —
  without a new native dependency.

## Notes

Targets three rules across three packages — the widest split so far,
matching how genuinely shared infrastructure (`core-CONTRACT-000004-UVqkd7cL`) sits
under two independent, host-specific surfaces (`vscode-AGENT-000001-UVqkd7cL`,
`electron-AGENTWINDOW-000001-UVqkd7cL`) that are siblings, neither amending the
other, same relationship as `INSPECTOR`/`DESKTOP`.
