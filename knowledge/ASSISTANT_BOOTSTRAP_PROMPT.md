# Assistant Bootstrap Prompt (Cross-Provider)

Paste this at the start of any AI session for this project.

---

You are collaborating on the **Synthalia** repository — an ESPHome firmware for an ESP32-S3 controlling 300 WS2812B LEDs with gesture-based interaction via a VL53L1X ToF sensor.

Use `knowledge/` as the public, shared memory layer for all assistants.

## At Session Start

1. Ensure `knowledge/` exists with exactly these files:
   - `knowledge/README.md`
   - `knowledge/ASSISTANT_BOOTSTRAP_PROMPT.md`
   - `knowledge/PROJECT_KNOWLEDGE.md`
   - `knowledge/DECISIONS.md`
2. If any file is missing, create it using the conventions in `knowledge/README.md`.
3. Read `knowledge/PROJECT_KNOWLEDGE.md` in full.
4. Read the latest 3 entries in `knowledge/DECISIONS.md`.
5. Run `git status` before making any changes.
6. Always validate config before suggesting a flash: `python3 -m esphome config s3-synthalia.yaml`

## Operating Rules

- Keep changes minimal, verifiable, and directly tied to the request.
- Never write secrets in tracked files, logs, or commit messages.
- Never write local/private metadata in `knowledge/` (paths, IPs, ports, serial IDs, hostnames).
- Replace sensitive/runtime-specific values with placeholders (`<DEVICE_IP>`, `<API_KEY>`, etc.).
- Validate ESPHome config after every change to `s3-synthalia.yaml` before proposing OTA.

## How to Write in `knowledge/`

- `PROJECT_KNOWLEDGE.md`: only stable technical facts, defaults, recurring gotchas.
- `DECISIONS.md`: append short ADR-style entries (date, context, decision, impact).
- Keep entries concise; avoid raw terminal transcripts.

## At Session End

Report:

1. Files changed.
2. Behavior impact.
3. Verification performed (`python3 -m esphome config` result).
4. Residual risks / follow-ups.

Then:

- Stable reusable fact discovered → write to `knowledge/PROJECT_KNOWLEDGE.md`.
- Architectural or operational decision made → append to `knowledge/DECISIONS.md`.
- Private/ephemeral notes → write to your provider's local memory, never to `knowledge/`.

---
