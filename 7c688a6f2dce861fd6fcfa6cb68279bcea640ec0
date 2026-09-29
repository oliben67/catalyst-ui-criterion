# `REQ-000012-UVqkd7cL` — Minimum framework version enforcement

A requirement stands on its own: vetted against every existing rule
document before being opened, always carries a `Domain`, and always
targets or proposes one or more rules.

| Field | Value |
|---|---|
| **ID** | `REQ-000012-UVqkd7cL` |
| **Name** | `minimum-framework-version-enforcement` |
| **Filename** | `REQ-000012-minimum-framework-version-enforcement.md` |
| **Status** | Completed |
| **Opened** | 2026-09-20 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL`, `vscode-ONBOARDING-000002-UVqkd7cL` |
| **Domain** | `ONBOARDING` |
| **Steps** | `STEP-000005-UVqkd7cL`, `STEP-000006-UVqkd7cL` |
| **Tests** | `TEST-000002-UVqkd7cL` |
| **Signed-off-by** | Olivier Steck |

## Description

Investigating "where do we enforce that the UI uses a minimum version
of catalyst framework" found there was no floor at all —
`MAX_COMPATIBLE_FRAMEWORK_VERSION` (`catalyst-host-vscode`) is a
ceiling used only to decide whether to *offer* a `/sync-framework`
action; nothing refused to load, parsed, or warned because a deployed
framework was *below* anything `catalyst-core`'s parser actually
assumes. This requirement adds a real, declared floor, described as a
version specifier the same way a `uv.lock`'s `requires-python` field
states one (`">=0.31.0"`) rather than a bare number whose meaning has
to be inferred, and surfaces it through the existing sync-offer
notification rather than adding a second, redundant one.

## Acceptance

- `catalyst-core` exposes `parseVersionSpecifier`/
  `satisfiesVersionSpecifier`, parsing and evaluating one version
  specifier clause (`>=`, `<=`, `==`, `!=`, `>`, `<`) against
  `compareVersions`.
- `catalyst-core` declares `REQUIRED_FRAMEWORK_VERSION = ">=0.31.0"` —
  the newest framework version its parser/graph/validator logic was
  actually verified against — plus `meetsRequiredFrameworkVersion`,
  which treats an unreadable `version.txt` (`null`) as satisfying the
  requirement rather than a false failure.
- `catalyst-host-vscode`'s existing sync-offer notification
  (`offerToSyncFramework`) shows exactly one message either way, never
  two popups for the same situation: the softer "supports syncing to"
  wording between the required floor and
  `MAX_COMPATIBLE_FRAMEWORK_VERSION`, and an explicit "below the
  required version — may not parse correctly" wording under the
  required floor.
- Still advisory — a dismissible offer, not a hard refusal to activate
  — consistent with the framework's own advisory-not-blocking posture
  elsewhere (`IAM`/role checks, INV-16).
- Full test coverage: the specifier parser/evaluator
  (`versioning.test.ts`) and `meetsRequiredFrameworkVersion`
  (`discover.test.ts`).

## Notes

Extends `core-CONTRACT-000001-UVqkd7cL`'s existing scope (the same
treatment `REQ-000010-UVqkd7cL`/`REQ-000011-UVqkd7cL` gave it for
`STEP-`/`TEST-` parsing) rather than a new rule there. `vscode-
ONBOARDING-000002-UVqkd7cL` is new: `vscode-ONBOARDING-000001-UVqkd7cL`
only covers the *no resolvable deployment* case; enforcing a minimum
on a deployment that *does* resolve, just on an older framework
version, is a distinct capability under the same domain, not an
amendment of `-000001`'s own promise. While extending
`core-CONTRACT-000001-UVqkd7cL`'s text, also corrected its stale
mention of a step's parent field as `Requirement` — renamed to
`Parent` by framework `0.31.0`, already reflected in the actual code
since `REQ-000011-UVqkd7cL`'s work but never updated in this rule's own
prose until now.

**Backfilled 2026-09-20**, after the fact: this requirement, both
steps, and the test were written up once the implementation was
already done and committed (`58aa794`), not opened as the work itself
started. Flagged explicitly per `Rules-of-Rules.md` §23/INV-29 (added
earlier this same session) rather than silently presented as if it had
been tracked in real time — it wasn't.

Verified: `npx tsc --build --force` clean; full monorepo `npm test`:
`catalyst-core` 203/203, `catalyst-host-electron` 16/16 (unaffected),
`catalyst-host-vscode` 79/79, `catalyst-ui` 25/25 — 323 tests total,
all green. `npm run lint` and `npm run format:check` clean.
