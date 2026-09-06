# `RUN-NNNNNN` — short title

> Copy this file to `runs/templates/TEMPLATE-RUN-v1.md` and resolve every `{{PLACEHOLDER}}` (INV-20). See `INSTANTIATION-GUIDE.md`.

A run is an agent's own live record of one task in progress — emitted
and mutated in place as the agent works, not created or edited by the
UI. The chain inspector watches this file the same way it watches
everything else in the corpus, so each save is a live update to its
run-monitor section. Permanent, never-reused ID — same scheme as every
other artifact type, though (unlike a proposal) picking one is the
agent's own responsibility, since no UI mediates its creation.

| Field | Value |
|---|---|
| **ID** | `RUN-NNNNNN` |
| **Filename** | descriptive kebab-case filename, e.g. `RUN-000001-sync-framework.md` |
| **Status** | running / completed / failed |
| **Command** | the command or task this run represents |
| **Started** | YYYY-MM-DDTHH:MM:SSZ |

## Checklist

One glyph-prefixed step per line, updated in place as the run
progresses:

- `✅` done
- `❌` failed
- `⏳` pending
- `⚠️` drift — the agent's own signal that something departed from
  expectation; not independently verified by the validator or by any
  host, the same way a proposal's `Expectations` aren't executed by
  this deployment either.

## Ledger

Free-text entries, one per line, in the order they happened — can cite
other ids (e.g. `` `PROP-000007` ``), picked up by the same
id-reference resolution as every other section.
