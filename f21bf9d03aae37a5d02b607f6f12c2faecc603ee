# `REQ-000008-UVqkd7cL` — Multi-root workspace support + install-offer

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000008-UVqkd7cL` |
| **Name** | `multi-root-and-install-offer` |
| **Filename** | `REQ-000008-multi-root-and-install-offer.md` |
| **Status** | done |
| **Opened** | 2026-09-06 |
| **Targets** | `vscode-INSPECTOR-000001-UVqkd7cL`, `vscode-ONBOARDING-000001-UVqkd7cL` |
| **Domain** | `ONBOARDING` |
| **Feature** | `FEAT-000008-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Extend `catalyst-host-vscode` to resolve, watch, and display a
deployment per workspace folder instead of only the first one
(amending `vscode-INSPECTOR-000001-UVqkd7cL`), and to offer an actionable
instantiation prompt when a folder has none (`vscode-ONBOARDING-000001-UVqkd7cL`,
new).

## Acceptance

- Every workspace folder is independently resolved via
  `resolveCorpusRoot`; each resolved folder gets its own `watchCorpus`
  instance, `DefinitionProvider`, `CodeLensProvider`, and
  `CodeActionsProvider`.
- With exactly one resolved deployment, the sidebar tree's root looks
  exactly as it does today (no added grouping level). With more than
  one, the root shows one collapsible entry per deployment, named
  after its workspace folder.
- `catalyst.showNodeDetail` resolves the right deployment's model
  (node ids are only unique within one corpus). `catalyst.
  composeProposal` prompts for which folder when there's more than
  one open deployment.
- A validation issue in one deployment's diagnostics never clears or
  is cleared by another deployment's diagnostics.
- Folders added to or removed from the workspace at runtime are picked
  up without an extension reload (`onDidChangeWorkspaceFolders`).
- A workspace folder with no resolvable `*.catalyst` shows an
  information message offering to copy an instantiation prompt to the
  clipboard (naming a discovered-or-configured framework repo
  location) — dismissible per folder via "Don't ask again," never
  auto-running anything.

## Notes

Targets two rules: `vscode-INSPECTOR-000001-UVqkd7cL` (amended in place — this is
an extension of what it already promises, not a new capability, same
treatment as the CodeLens wording correction in Phase 3) and the new
`vscode-ONBOARDING-000001-UVqkd7cL` (a genuinely new capability). No `catalyst-
core` or `catalyst-host-electron` changes — `resolveCorpusRoot`/
`watchCorpus` are already per-corpus-root.
