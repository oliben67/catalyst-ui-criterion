# Runs

`RUN-NNNNNN` docs — an agent's own live run-state, emitted and mutated
in place as it works, giving the chain inspector's run monitor
(`RM-000007`) a live checklist and ledger to watch. Deployment-local
artifact type, not a catalyst framework-wide concept — `packages/
catalyst-core` (in the `catalyst-ui` product) is what knows how to parse
this directory, the same way a deployment can define a new rule domain
on its own. Unlike `proposals/`, the UI never creates or edits a run
file — only the agent does; the UI only reads and displays. None yet;
`runs.md` is the index and `templates/TEMPLATE-RUN-v1.md` the template.
See `rules/catalyst-core-rules.md` (`core-CONTRACT-003`) and
`rules/catalyst-host-vscode-rules.md` (`RUNMONITOR` domain).
