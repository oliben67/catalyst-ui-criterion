# Deployment Note

- Framework: catalyst framework
- Deployed project: catalyst-ui (`git@github.com:oliben67/catalyst-ui.git`)
- Working copy (`.criterion/`): this directory — agent-owned space,
  computed per machine per `BOOTSTRAP.md` §1 (Claude Code's per-project
  data directory for this project), reached through the gitignored
  `catalyst-ui/.criterion` symlink; no tracked file records its path
  (kernel 0.37.0, INV-6)
- Originally instantiated: 2026-09-05 (greenfield path —
  `development-framework/INSTANTIATION-GUIDE.md` §3 — no application
  code existed yet; dev-environment decisions established as this
  deployment's first rule document, `rules/dev-environment-rules.md`,
  before any product code)
- `version.txt`: `0.17.0` at instantiation; currently `0.39.0` (see
  version history below).
- catalyst CLI: vendored at `bin/catalyst.pyz` (kernel 0.39.0,
  `CLI.md`); `catalyst hook stop` registered as the Claude Code Stop hook
  in the project's `.claude/settings.json`.

## Process module (`MODULE-SPECIFICATION.md` §6)

- module: `software-engineering` (named in `catalyst-ui.catalyst`'s `module` field)
- module version: `2.1.0` — seeded whole-tree into `modules/software-engineering/` from the
  module's v2.0.0 release archive, refreshed to 2.1.0 on 2026-09-27 with
  the kernel 0.38.0 sync (manifest `kernelVersion: >=0.38.0`)
- composed into `CODE-OF-CONDUCT.md` §3/§4, `rules/Rules-of-Rules.md` and
  `Taskfile.common.yml` under `From module software-engineering` blocks by
  `/sync-framework` (kernel 0.36.0 migration, applied 2026-09-27)

## Repo sync (criterion, `Rules-of-Rules.md` §13)

- repoed: true
- catalyst_repo: catalyst-ui-criterion
- catalyst_repo_url: git@github.com:oliben67/catalyst-ui-criterion.git
- created_by: Olivier Steck
- criterion_branch: criterion — the shared branch. Since kernel 0.39.0
  (2026-09-27) `.criterion` is a git submodule of the catalyst-ui
  repository and changes land through pull requests (`catalyst criterion
  push`); the repository's CI runs `catalyst check` and the integrity check.
  Branch protection is enabled (2026-09-28, after the criterion repository
  was made public): pull requests and the `catalyst` check are required on
  `criterion`; force pushes and deletion are blocked. Admins are not forced
  through it (enforce_admins off).

Mirrored into `catalyst-ui.catalyst` at the project root
(`Rules-of-Rules.md` §14) — this file is the source of record if the
two ever disagree. Initial commit `2e1941b` pushed 2026-09-05.

## Version history

- 2026-09-27 — kernel `0.37.0` → `0.38.0` (`migrations/0.38.0/catalyst-cli.md`):
  catalyst CLI vendored, `catalyst` task added to `Taskfile.common.yml`,
  `catalyst hook stop` registered, `CODE-OF-CONDUCT.md`/`rules/Rules-of-Rules.md`
  recomposed, `.claude/commands/` refreshed, journal blobs pinned under
  `refs/catalyst/journal`; module `software-engineering` 2.0.0 → 2.1.0.
  Part of catalyst beta-readiness RM-000013.
- 2026-09-27 — 0.39.0: kernel files synced; submodule conversion pending
  (`migrations/0.39.0/criterion-on-git.md`). Part of catalyst beta-readiness RM-000014.
- 2026-09-28 — kernel 0.40.0, module software-engineering 2.2.0 (explicit install, ceremony tiers, `catalyst spec`): documents recomposed with `catalyst recompose` (no conflicts); CLI re-vendored; command files refreshed.
- 2026-09-28 — kernel 0.41.0 (traced commits, format 1.0-rc, catalyst report): documents recomposed; CLI re-vendored; CI runs catalyst trace; commit-msg hook installed.
- 2026-09-29 — kernel 0.42.1, module software-engineering 2.3.0 (changes made outside catalyst: `catalyst unrecorded`, `/adopt`, `journal adopt`; baseline `journal_since` at c4bda0cc09): documents recomposed with `catalyst recompose` (no conflicts); module refreshed from the 2.3.0 release; `TEMPLATE-RECONCILIATION-v3`; `/adopt` command file; CLI re-vendored.
- 2026-09-30 — kernel 0.44.0 (0.42.2 reproducible archives; 0.43.0 `criterion create` without a URL; 0.44.0 four-eyes analysis, migration 0.44.0): documents recomposed with `catalyst recompose` (no conflicts); `analyses/`, `definitions/analysis.md`, `ANALYSIS-PLAYBOOK.md` deployed; `/run-analysis` and `/criterion` command files refreshed; CLI re-vendored.
- 2026-10-01 — kernel 0.45.0 (0.44.1: a module release states its kernel; 0.45.0: what a deployment governs, migration 0.45.0), module software-engineering 2.3.1: documents recomposed (no change); module refreshed from its release; CLI re-vendored. The commit-msg hook reinstall (migration step 2) is left for the user's assent.
