# Roles

`roles.json` — the role → typical-action mapping (`Rules-of-Rules.md` §11), seeded with a default agile-role set and extended via `/role-add`/`/role-modify`. Never hand-edited otherwise.

See `templates/` for the registry's versioned seed shape (`TEMPLATE-ROLES-vN.json`) — it versions the seed content a fresh `roles.json` starts from, not a per-instance document, since the whole registry is one JSON array rather than one-file-per-instance.
