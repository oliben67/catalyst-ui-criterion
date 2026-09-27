# Dev-environment rules

The foundational tooling, stack, and dev-environment decisions for
catalyst-ui, established as rules before the first line of application
code — catalyst's greenfield instantiation path
(`development-framework/INSTANTIATION-GUIDE.md` §3 in the catalyst
framework repository). Each rule is implemented in the same pass it's
defined: the config file it describes actually exists in this
repository, and the tool/CI it names actually runs clean against the
still-empty scaffold — that is this rule set's "tested" bar
(`Rules-of-Rules.md` §2), not a unit test.

## Contents

- [`RUNTIME`](#runtime) — `env-RUNTIME-001`
- [`LAYOUT`](#layout) — `env-LAYOUT-001`
- [`DEPS`](#deps) — `env-DEPS-001`
- [`STYLE`](#style) — `env-STYLE-001`
- [`TEST`](#test) — `env-TEST-001`
- [`CI`](#ci) — `env-CI-001`
- [`DX`](#dx) — `env-DX-001`

## `RUNTIME`

> **Domain:** `RUNTIME` — see [domains/env-RUNTIME-language-and-runtime.md](domains/env-RUNTIME-language-and-runtime.md).

### `env-RUNTIME-001` Language and runtime

✅ working. Every package in this repository is TypeScript, compiled
against Node.js 20 LTS, with `strict: true` in `tsconfig.json`.
Implemented: root `tsconfig.base.json` (`compilerOptions.strict: true`,
`target`/`module` set for Node 20), each package's own `tsconfig.json`
extending it. Tested: `tsc --noEmit` runs clean against the empty
scaffold.

## `LAYOUT`

> **Domain:** `LAYOUT` — see [domains/env-LAYOUT-repo-and-module-layout.md](domains/env-LAYOUT-repo-and-module-layout.md).

### `env-LAYOUT-001` npm workspaces monorepo

✅ working. This repository is an npm-workspaces monorepo with four
packages: `packages/catalyst-core` (parser/model/validator/watcher, no
DOM), `packages/catalyst-ui` (React, mounted by both hosts),
`packages/catalyst-host-vscode` and `packages/catalyst-host-electron`
(thin protocol adapters) — matching the project's own roadmap
architecture. Implemented: root `package.json`'s `workspaces` field
listing `packages/*`; each package has its own `package.json`. Tested:
`npm install` resolves all four workspaces with no errors.

## `DEPS`

> **Domain:** `DEPS` — see [domains/env-DEPS-dependency-policy.md](domains/env-DEPS-dependency-policy.md).

### `env-DEPS-001` Locked, ordinary semver dependencies

✅ working. Dependencies are added with ordinary semver ranges (`^` by
default) and locked via a single root `package-lock.json`, committed.
No additional vetting process for now — revisit if/when the project
grows a security-sensitive dependency surface. Implemented: root
`package-lock.json`. Tested: `npm ci` installs reproducibly from the
lockfile with no errors.

## `STYLE`

> **Domain:** `STYLE` — see [domains/env-STYLE-code-style.md](domains/env-STYLE-code-style.md).

### `env-STYLE-001` ESLint + Prettier

✅ working. Linting via ESLint with `typescript-eslint`; formatting via
Prettier; both run against every workspace from the root. Implemented:
root `.eslintrc.cjs`, root `.prettierrc.json`. Tested: `npm run lint`
and `npm run format:check` both exit zero against the empty scaffold.

## `TEST`

> **Domain:** `TEST` — see [domains/env-TEST-testing.md](domains/env-TEST-testing.md).

### `env-TEST-001` Vitest for core/UI; VS Code's own harness for the VS Code host

✅ working. `catalyst-core` and `catalyst-ui` use Vitest (fast,
ESM-native, no DOM required for `catalyst-core`; `jsdom` environment
available to `catalyst-ui`, exercised in its own scaffold test).
`catalyst-host-vscode` uses Mocha, run directly against its compiled
output for now — `@vscode/test-electron` is declared as a
devDependency and wires in once real `activate()` logic exists to
integration-test against a launched VS Code instance (roadmap Phase 2);
until then, launching a full VS Code instance to test an empty
extension has nothing to verify. `catalyst-host-electron` has no test
setup yet; deferred to when that package gets real code (roadmap Phase
6). Test locations: `packages/<name>/src/**/*.test.ts` (Vitest
packages), `packages/catalyst-host-vscode/src/test/**/*.test.ts` (Mocha
suite). This resolves `Rules-of-Rules.md` §2's `{{TEST_LOCATIONS}}` for
every rule created in this repository from now on. Implemented: each
Vitest package's `vitest.config.ts`; `catalyst-host-vscode`'s Mocha
setup (`src/test/extension.test.ts`, run via `npm run test` after a
`pretest` build step). Tested, actually run and verified during this
instantiation: `npm run lint`, `npm run format:check`, `npm run
typecheck`, and `npm test` (3 suites, 3 tests) all exit zero.

## `CI`

> **Domain:** `CI` — see [domains/env-CI-ci-cd.md](domains/env-CI-ci-cd.md).

### `env-CI-001` GitHub Actions gate: lint, typecheck, test

✅ working. Every push and pull request runs lint, typecheck
(`tsc --noEmit` across all workspaces), and test (`npm test`) via
GitHub Actions; all three must pass to merge. Implemented:
`.github/workflows/ci.yml`. Tested: the workflow is present and
syntactically valid; full green-run verification happens on first push
to GitHub (outside this local scaffold pass).

## `DX`

> **Domain:** `DX` — see [domains/env-DX-local-dev-environment.md](domains/env-DX-local-dev-environment.md).

### `env-DX-001` Pinned Node version, no devcontainer yet

✅ working. Node version is pinned via `.nvmrc` (`20`) so `nvm use`
matches CI. No devcontainer/Docker Compose/Nix setup yet — revisit if
the toolchain grows environment-sensitive dependencies. No required
environment variables or secrets exist yet. Implemented: root
`.nvmrc`. Tested: `cat .nvmrc` matches the CI workflow's configured
Node version.

## Known Bugs — Quick Index

*(none yet — this is a fresh greenfield instantiation, not an audit of
a running system)*
