# Project Memory (Synthalia)

## Note

Stable project facts (stack, commands, gotchas, architecture) have moved to `knowledge/PROJECT_KNOWLEDGE.md`.
Decisions log is now in `knowledge/DECISIONS.md`.
Read those first — this file retains only Codex-specific behavioral rules and the pre-flight checklist.

## Core Directives
- Never write secrets in plaintext in tracked files, output, or commit messages.
- Before firmware edits, always validate with `python3 -m esphome config s3-synthalia.yaml`.
- For OTA/logs, always pass an explicit device (`--device <DEVICE_IP>`).
- Prefer minimal, testable changes with easy rollback.
- Update `knowledge/PROJECT_KNOWLEDGE.md` for stable facts; update this file only for Codex-specific rules.

## Working Preferences
- Practical, concise communication.
- Security and consistency first, optimization second.
- Prefer small patches + immediate OTA/log verification.
- Avoid broad refactors unless explicitly requested.

## Pre-Flight Checklist
- [ ] Read `knowledge/PROJECT_KNOWLEDGE.md` and the last 2–3 entries of `knowledge/DECISIONS.md`.
- [ ] Read the last 2 entries of `SESSION_LOG.md`.
- [ ] No plaintext secrets in changes or notes.
- [ ] `secrets.yaml` is still ignored and not staged.
- [ ] `python3 -m esphome config s3-synthalia.yaml` passes.
- [ ] If gesture/light logic changed: run OTA + logs test.
- [ ] Append session notes to `SESSION_LOG.md` at end of work.
