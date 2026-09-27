# Rules index

Global index of every rule document and rule ID in this deployment. Per
`Rules-of-Rules.md` §5, no rule is valid unless listed here.

## Rule documents

| Prefix | Document | Domains |
|---|---|---|
| `env` | [`dev-environment-rules.md`](dev-environment-rules.md) | `RUNTIME`, `LAYOUT`, `DEPS`, `STYLE`, `TEST`, `CI`, `DX` |
| `core` | [`catalyst-core-rules.md`](catalyst-core-rules.md) | `CONTRACT` |
| `vscode` | [`catalyst-host-vscode-rules.md`](catalyst-host-vscode-rules.md) | `INSPECTOR`, `HEALTH`, `PROPOSAL`, `RUNMONITOR`, `ONBOARDING`, `AGENT` |
| `electron` | [`catalyst-host-electron-rules.md`](catalyst-host-electron-rules.md) | `DESKTOP`, `AGENTWINDOW` |

## Rule IDs

- `env-RUNTIME-000001-UVqkd7cL` — Language and runtime
- `env-LAYOUT-000001-UVqkd7cL` — npm workspaces monorepo
- `env-DEPS-000001-UVqkd7cL` — Locked, ordinary semver dependencies
- `env-STYLE-000001-UVqkd7cL` — ESLint + Prettier
- `env-TEST-000001-UVqkd7cL` — Vitest for core/UI; VS Code's own harness for the VS Code host
- `env-CI-000001-UVqkd7cL` — GitHub Actions gate: lint, typecheck, test
- `env-DX-000001-UVqkd7cL` — Pinned Node version, no devcontainer yet
- `core-CONTRACT-000001-UVqkd7cL` — Typed chain model, global validation, watched changes
- `core-CONTRACT-000002-UVqkd7cL` — Proposal parsing and reconciliation-state tracking
- `core-CONTRACT-000003-UVqkd7cL` — Run-state parsing
- `core-CONTRACT-000004-UVqkd7cL` — Agent-command and slash-command discovery
- `vscode-INSPECTOR-000001-UVqkd7cL` — Read-only chain tree and node-detail webview
- `vscode-HEALTH-000001-UVqkd7cL` — Diagnostics, click-to-jump, and CodeLens for corpus files
- `vscode-PROPOSAL-000001-UVqkd7cL` — Propose-fix code action and pending badges
- `vscode-PROPOSAL-000002-UVqkd7cL` — Authoring composer
- `vscode-RUNMONITOR-000001-UVqkd7cL` — Live run checklist and ledger
- `vscode-ONBOARDING-000001-UVqkd7cL` — Offer to install catalyst when no deployment is found
- `vscode-ONBOARDING-000002-UVqkd7cL` — Offer to sync, and warn below a minimum, when a deployment resolves but is outdated
- `vscode-AGENT-000001-UVqkd7cL` — Run catalyst slash commands via a per-project agent terminal
- `electron-DESKTOP-000001-UVqkd7cL` — Multi-project tracking, persistent watch, and graph view
- `electron-AGENTWINDOW-000001-UVqkd7cL` — Run catalyst slash commands via a per-project agent window
