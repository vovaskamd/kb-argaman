## Repo rules for Codex/agents

- Source of truth for knowledge is `kb/sections/*.md`.
- Keep `site/docs/sections/*.md` in sync (only for published sections).
- Do not introduce PII/secrets into Git (phones, IDs, chats, client data). Put such data in `kb/private/` (ignored).
- Never commit `node_modules/`, build artifacts, or OS junk (`.DS_Store`).
- Prefer small, reviewable commits with clear messages.
