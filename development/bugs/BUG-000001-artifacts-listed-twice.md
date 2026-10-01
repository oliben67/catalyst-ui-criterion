# `BUG-000001-UVqkd7cL` — Every artifact listed twice in the chain tree

| Field | Value |
|---|---|
| **ID** | `BUG-000001-UVqkd7cL` |
| **Name** | `artifacts-listed-twice` |
| **Filename** | `BUG-000001-artifacts-listed-twice.md` |
| **Status** | Fixed |
| **Severity** | High |
| **Opened** | 2026-10-02 |
| **Targets** | `core-CONTRACT-000001-UVqkd7cL` |
| **Domain** | `CONTRACT` |
| **Area** | `catalyst-core` parser (`parser.ts` `filesById`) |
| **Steps** | *(none)* |
| **Signed-off-by** | Olivier Steck |

## Description

The chain model shows each requirement (and step, feature) twice: one node
from its file, one index-only node from its index row. The kernel's
`catalyst index regen` (0.38.0+) writes index rows with the full ID
(`REQ-000014-UVqkd7cL`), while this deployment's files are named without
the userid (`REQ-000014-entity-references-are-links.md`); the parser keys a
file by the ID in its filename (`REQ-000014`), so the two never match. A
node's downstream list then includes itself.

## Reproduction

Open the chain inspector on catalyst-ui (Extension Development Host,
2026-10-02): Requirements lists "`detail panels one group per project`"
and "Detail panels: at most one editor group per project" for
`REQ-000013`; its Produces list includes `REQ-000013`.

## Expected vs actual

- **Expected** (per the targeted rule): one typed node per artifact — its
  file and its index row are the same artifact.
- **Actual**: two nodes, keyed `REQ-000014` and `REQ-000014-UVqkd7cL`.

## Root cause

`packages/catalyst-core/src/parser.ts` `filesById`: the key comes from the
filename only.

## Fix plan

Implementation: key a file by the full ID in its own `ID` field (the
filename is the fallback), and merge a file keyed by a short ID with the one
full index ID that extends it.

## Fix

`filesById` keys a file by the full ID in its own `ID` field, else by its
filename, merging a short filename ID with the one full index ID that
extends it (`parser.ts` `canonicalFileId`), for requirements, bugs,
house-keeping, tests, features and steps alike. Verified in a running
Extension Development Host on catalyst-ui (2026-10-02): 17 requirement rows
for 17 IDs. Same day: hover descriptions fall back to a node's
`## Description` / `## Summary` section (`describeFromContent`), and hovers
show the readable title rather than the slug.

## Test plan

`packages/catalyst-core/src/test/parser.test.ts`: a file named without the
userid and an index row with the full ID give one node.

## Related

`REQ-000014-UVqkd7cL` (entity links, where it showed).
