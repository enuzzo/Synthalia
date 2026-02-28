# .codex Usage

This folder is Codex-specific operational context. Stable, public project knowledge now lives in `knowledge/` (the canonical cross-provider layer).

## File Roles
- `MEMORY.md`: Codex-specific rules and pre-flight checklist. Stable project facts live in `knowledge/PROJECT_KNOWLEDGE.md`.
- `SESSION_LOG.md`: append-only chronological log of sessions, errors, and fixes (private operational context).

## Start-Of-Session Ritual
- Read `knowledge/PROJECT_KNOWLEDGE.md` and the latest entries in `knowledge/DECISIONS.md` (canonical source of truth).
- Read `MEMORY.md` for Codex-specific behavioral rules.
- Read the last 2 entries in `SESSION_LOG.md`.
- Align planned changes with those rules before touching code/config.

## End-Of-Session Ritual
- Append a new entry in `SESSION_LOG.md` (goal, errors, fixes, checks, follow-ups).
- Update `MEMORY.md` only when a rule is stable and reusable.
- Keep changes minimal and verified.

## Security (Mandatory)
- Absolute ban on secrets in `.codex/*`.
- No passwords/tokens/API keys in output or commit messages.
- Secrets stay only in local git-ignored files (e.g. `secrets.yaml`).
