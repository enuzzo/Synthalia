# .codex Usage

This folder stores project memory and operational notes, with no sensitive data.

## File Roles
- `MEMORY.md`: stable rules, consolidated decisions, and pre-flight checklist.
- `SESSION_LOG.md`: append-only chronological log of sessions, errors, and fixes.

## Start-Of-Session Ritual
- Read `MEMORY.md`.
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
