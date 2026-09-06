# Rules index

Global index of every rule document and rule ID in this deployment. Per
`Rules-of-Rules.md` §5, no rule is valid unless listed here.

## Rule documents

| Prefix | Document | Domains |
|---|---|---|
| `env` | [`dev-environment-rules.md`](dev-environment-rules.md) | `RUNTIME`, `LAYOUT`, `DEPS`, `STYLE`, `TEST`, `CI`, `DX` |
| `core` | [`catalyst-core-rules.md`](catalyst-core-rules.md) | `CONTRACT` |
| `vscode` | [`catalyst-host-vscode-rules.md`](catalyst-host-vscode-rules.md) | `INSPECTOR`, `HEALTH`, `PROPOSAL`, `RUNMONITOR` |
| `electron` | [`catalyst-host-electron-rules.md`](catalyst-host-electron-rules.md) | `DESKTOP` |

## Rule IDs

- `env-RUNTIME-001` — Language and runtime
- `env-LAYOUT-001` — npm workspaces monorepo
- `env-DEPS-001` — Locked, ordinary semver dependencies
- `env-STYLE-001` — ESLint + Prettier
- `env-TEST-001` — Vitest for core/UI; VS Code's own harness for the VS Code host
- `env-CI-001` — GitHub Actions gate: lint, typecheck, test
- `env-DX-001` — Pinned Node version, no devcontainer yet
- `core-CONTRACT-001` — Typed chain model, global validation, watched changes
- `core-CONTRACT-002` — Proposal parsing and reconciliation-state tracking
- `core-CONTRACT-003` — Run-state parsing
- `vscode-INSPECTOR-001` — Read-only chain tree and node-detail webview
- `vscode-HEALTH-001` — Diagnostics, click-to-jump, and CodeLens for corpus files
- `vscode-PROPOSAL-001` — Propose-fix code action and pending badges
- `vscode-PROPOSAL-002` — Authoring composer
- `vscode-RUNMONITOR-001` — Live run checklist and ledger
- `electron-DESKTOP-001` — Multi-project tracking, persistent watch, and graph view
