## Repo rules for Codex/agents

- Source of truth for knowledge is `kb/sections/*.md`.
- Keep exports in sync when editing a section:
  - `site/docs/sections/*.md` (only for published sections)
  - `kb/vector_upload/*.txt` and `kb/vector_upload.csv`
- Do not introduce PII/secrets into Git (phones, IDs, chats, client data). Put such data in `kb/private/` (ignored).
- Never commit `node_modules/`, build artifacts, or OS junk (`.DS_Store`).
- Prefer small, reviewable commits with clear messages.

