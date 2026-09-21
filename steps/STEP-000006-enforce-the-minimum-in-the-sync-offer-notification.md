# `STEP-000006-UVqkd7cL` — Enforce the minimum in the sync-offer notification

| Field | Value |
|---|---|
| **ID** | `STEP-000006-UVqkd7cL` |
| **Name** | `enforce-the-minimum-in-the-sync-offer-notification` |
| **Filename** | `STEP-000006-enforce-the-minimum-in-the-sync-offer-notification.md` |
| **Parent** | `REQ-000012-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-09-20 |
| **Closed** | 2026-09-20 |
| **Tests** | `TEST-000002-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Surface `REQUIRED_FRAMEWORK_VERSION` (from `STEP-000005-UVqkd7cL`) to
the user in `catalyst-host-vscode`, without adding a second notification
alongside the existing `MAX_COMPATIBLE_FRAMEWORK_VERSION` sync offer —
the enforcement/UI half of `REQ-000012-UVqkd7cL`.

## Actions performed

- `packages/catalyst-host-vscode/src/extension.ts`: `offerToSyncFramework`
  now branches its message text on `meetsRequiredFrameworkVersion`
  instead of always using the same "supports syncing to" wording — below
  the required floor the message says so explicitly ("may not parse
  correctly"), at or above it (but still below
  `MAX_COMPATIBLE_FRAMEWORK_VERSION`) the wording is unchanged. Same
  notification, same dismiss/"Sync now" flow either way — one popup per
  situation, never two.
- Deliberately did not add a hard refusal to activate: kept the existing
  advisory, dismissible-offer posture, consistent with the framework's
  own advisory-not-blocking stance elsewhere (`IAM`/role checks, INV-16).

## Verification

`npx tsc --build --force` clean across every workspace; full monorepo
`npm test`: `catalyst-core` 203/203, `catalyst-host-electron` 16/16
(unaffected), `catalyst-host-vscode` 79/79 (unaffected —
`offerToSyncFramework` has no direct unit tests, it's `vscode`-API-bound
same as the rest of `extension.ts`), `catalyst-ui` 25/25 — 323 total,
zero regressions. `npm run lint` and `npm run format:check` clean.

## Related

`STEP-000005-UVqkd7cL` (the data-model half, in `catalyst-core`).
