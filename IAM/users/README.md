# Users

`users.json` — the registry of people who can sign work (`Rules-of-Rules.md` §11). Managed only by `/user-add`/`/user-remove`/`/user-modify`/`/user-assign-role`/`/user-list` — never hand-edited.

See `templates/` for the registry's versioned seed shape (`TEMPLATE-USERS-vN.json`) — it versions the seed content a fresh `users.json` starts from, not a per-instance document, since the whole registry is one JSON array rather than one-file-per-instance.
