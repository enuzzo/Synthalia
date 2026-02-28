# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Shared Knowledge

At session start, read:

- `knowledge/PROJECT_KNOWLEDGE.md` — stable technical context, commands, hardware, and gotchas.
- `knowledge/DECISIONS.md` (latest entries) — architectural and operational decisions.

These files are the single source of truth for project-level facts. Do not duplicate their content here.

## Session Protocol

**Start:** Read `knowledge/PROJECT_KNOWLEDGE.md` + latest `knowledge/DECISIONS.md` entries → run `git status` → validate config before any flash suggestion.

**End:** Stable reusable fact → `knowledge/PROJECT_KNOWLEDGE.md`. Decision made → append to `knowledge/DECISIONS.md`. Ephemeral/private notes → local memory only (never versioned).

## Behavioral Rules

- Minimal, targeted changes — no broad refactors unless explicitly requested.
- Always validate before suggesting a flash: `python3 -m esphome config s3-synthalia.yaml`
- Never write secrets, local paths, or private infra details in any tracked file.
- Use `<DEVICE_IP>` placeholder in all commands and docs — never a real IP.
- Prefer small patches + OTA/log verification over large batches.
- `esphome` may not be in PATH — always use `python3 -m esphome`.
