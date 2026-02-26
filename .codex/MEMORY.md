# Project Memory (Synthalia)

## Core Directives
- Never write secrets in plaintext in tracked files, output, or commit messages.
- Before firmware edits, always validate with `python3 -m esphome config s3-synthalia.yaml`.
- For OTA/logs, always pass an explicit device (`--device <ip|hostname>`).
- Prefer minimal, testable changes with easy rollback.
- Update this memory only with stable, reusable rules.

## Working Preferences
- Practical, concise communication.
- Security and consistency first, optimization second.
- Prefer small patches + immediate OTA/log verification.
- Avoid broad refactors unless explicitly requested.

## Consolidated Technical Decisions
- Stack: ESPHome on `esp32-s3-devkitc-1` (Arduino framework).
- Main config: `s3-synthalia.yaml`.
- Runtime secrets: local `secrets.yaml` referenced via `!secret`.
- Standard commands:
  - Validate: `python3 -m esphome config s3-synthalia.yaml`
  - Build + OTA: `python3 -m esphome run s3-synthalia.yaml --device <IP>`
  - Live logs: `python3 -m esphome logs s3-synthalia.yaml --device <IP>`

## Security And Secrets
- Secrets live in local `secrets.yaml` (not versioned).
- `secrets.yaml` is excluded via `.gitignore`.
- Tracked files must contain references (`!secret ...`), never sensitive values.
- If `config.h` is introduced, keep it local/ignored and version only a clean template (`config.example.h`).

## Recurring Gotchas
- `esphome` may not be in `PATH`: use `python3 -m esphome`.
- `external_components` from GitHub needs network access.
- After node rename, first OTA may require direct IP instead of hostname.
- HYPOTHESIS: gesture can feel slow if filters/transitions are too aggressive.

## Pre-Flight Checklist
- [ ] Read this `MEMORY.md` and the last 2 entries of `SESSION_LOG.md`.
- [ ] No plaintext secrets in changes or notes.
- [ ] `secrets.yaml` is still ignored and not staged.
- [ ] `python3 -m esphome config s3-synthalia.yaml` passes.
- [ ] If gesture/light logic changed: run OTA + logs test.
- [ ] Append session notes to `SESSION_LOG.md` at end of work.
