# `STEP-000016-UVqkd7cL` — Link entity references in the webview

| Field | Value |
|---|---|
| **ID** | `STEP-000016-UVqkd7cL` |
| **Name** | `link-entity-references` |
| **Filename** | `STEP-000016-link-entity-references.md` |
| **Parent** | `REQ-000014-UVqkd7cL` |
| **Status** | done |
| **Opened** | 2026-10-01 |
| **Closed** | 2026-10-01 |
| **Tests** | *(none yet)* |
| **Signed-off-by** | Olivier Steck |

## Description

Implement `REQ-000014-UVqkd7cL`.

## Actions performed

- `catalyst-core` `types.ts`: `ReferenceInfo` (`id`, `kind`, `name`,
  `summary`) and `WebviewPayload.references`, keyed by the citing token.
- `catalyst-host-vscode` `detail.ts`: `buildReferenceTable()` (every node
  whose full ID occurs as a whole token, plus an unambiguous short form
  such as `REQ-000014`; never the panel's own node), `shortSummary()`
  (description without markdown, first sentence, ≤180 characters),
  `referencesForNode()`. `extension.ts`: node payloads (open and refresh)
  and the backlog carry the table; a panel's `openReference` message opens
  that entity in the same project, so it lands in the project's group
  (`REQ-000013-UVqkd7cL`).
- `catalyst-ui` `references.ts`: `linkifyReferences()` — known tokens in
  rendered HTML become `a.catalyst-ref` links with the hover as `title`;
  inline code linked, `<pre>` and existing links left alone; HTML-escaped.
  `NodeDetail` (details, upstream/downstream lists) and `Backlog` use it;
  `webview-entry.tsx` posts a clicked reference to the host
  (`acquireVsCodeApi`), the views stay host-agnostic. Exported from
  `index.ts`.

## Verification

`references.test.ts` (5), `NodeDetail.test.ts` (+1), host `detail.test.ts`
(+3). All workspaces: catalyst-core 240, electron 16, vscode host 88,
catalyst-ui 35 passing; tsc, eslint, prettier clean. Not exercised in a
running Extension Host.
