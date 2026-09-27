# `REQ-000006-UVqkd7cL` — Electron host

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000006-UVqkd7cL` |
| **Name** | `electron-host` |
| **Filename** | `REQ-000006-electron-host.md` |
| **Status** | done |
| **Opened** | 2026-09-05 |
| **Targets** | `electron-DESKTOP-000001-UVqkd7cL` |
| **Domain** | `DESKTOP` |
| **Feature** | `FEAT-000006-UVqkd7cL` |
| **Steps** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `catalyst-host-electron`'s multi-project tracking, persistent
per-project watch, and graph view (`electron-DESKTOP-000001-UVqkd7cL`), reusing
`catalyst-core`'s existing protocol and `catalyst-ui`'s `NodeDetail`
component unchanged.

## Acceptance

- A tracked-project list persists (add/remove) independently of which
  project is currently selected in the UI.
- One `watchCorpus` instance runs per tracked project concurrently — not
  torn down when switching the selected project.
- A graph view renders the selected project's chain model: every node
  and edge from the model appears, laid out deterministically (no
  overlapping/NaN positions), grouped so the four layers are visually
  distinguishable ("room to breathe," not a single dense mass).
- Selecting a node in the graph view shows `catalyst-ui`'s `NodeDetail`
  component, imported unchanged — no new file added to
  `packages/catalyst-ui` for this.
- Read-only: no proposal creation, no authoring composer from this
  host in this phase.

## Notes

Targets one rule only (`electron-DESKTOP-000001-UVqkd7cL`) — this phase doesn't
touch proposal/run-state infrastructure, so there's no second,
independent-infrastructure rule the way `REQ-000004-UVqkd7cL` targeted
`core-CONTRACT-000002-UVqkd7cL` alongside its host-specific rule.
