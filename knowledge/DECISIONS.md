# Decisions

Concise ADR-style log for stable project decisions. Append-only: do not edit past entries.

Entry format:

```
## YYYY-MM-DD - Title

- Context:
- Decision:
- Impact/Tradeoffs:
```

---

## 2026-02-26 - Canonical ESPHome Invocation via `python3 -m esphome`

- Context: `esphome` binary not found when called directly; Python bin directory absent from PATH in test environments.
- Decision: Standardized all commands to `python3 -m esphome` across all docs and session notes.
- Impact/Tradeoffs: Consistent across environments; slightly more verbose than a direct alias, but reliable.

---

## 2026-02-26 - Secrets Hygiene Baseline

- Context: Firmware connects to WiFi and Home Assistant; credentials must not land in git history.
- Decision: All credentials live in local `secrets.yaml` (git-ignored); YAML references them via `!secret <key>`; `.gitignore` enforces exclusion.
- Impact/Tradeoffs: No accidental credential commits; requires manual `secrets.yaml` creation on new machines.

---

## 2026-02-26 - English-First Public Documentation

- Context: Codebase was Italian-first internally; user wanted to publish to GitHub with English-primary documentation.
- Decision: `README.md`, `LICENSE`, and commit messages in English. Firmware YAML comments and log strings may remain in Italian.
- Impact/Tradeoffs: Better reach for public contributors; Italian firmware comments preserved for developer ergonomics.

---

## 2026-02-26 - Branch Protection on `main` (PR-Required Flow)

- Context: Repository published publicly on GitHub; direct pushes to `main` could corrupt history.
- Decision: Enabled branch protection: 1 PR review required, stale reviews dismissed on new push, force-push and branch deletion disabled.
- Impact/Tradeoffs: All changes go through PRs; adds friction for solo workflow but prevents history corruption. Can be relaxed if solo workflow becomes too strict.

---

## 2026-02-27 - Lowercase GitHub Repository Name

- Context: Repository was created as `enuzzo/Synthalia`; all-lowercase repo names preferred for URL uniformity. Branding (first-letter uppercase) stays in README.
- Decision: Renamed GitHub repo from `Synthalia` to `synthalia`. GitHub auto-redirects old URL.
- Impact/Tradeoffs: Cleaner URLs; redirect is transparent; local clones may optionally run `git remote set-url origin` to update.

---

## 2026-02-27 - Extended EFFECTS Mode from 4 to 7 Effects

- Context: Original firmware had 4 effects (indices 0–3); three new effects were designed and validated with `esphome config`.
- Decision: Added Interactive Plasma Vortex (4), Comet Rain (5), Nebula Spark (6); encoder navigation extended to range 0–6; `apply_effect` script and gesture logger updated accordingly.
- Impact/Tradeoffs: Richer interaction palette; firmware YAML grew; visual parameter tuning still needed on physical hardware. 3 slots remain open toward the 10-effect roadmap goal.

---

## 2026-02-28 - Introduce `knowledge/` Cross-Provider Knowledge Layer

- Context: `.codex/` was Codex-specific; project needed a portable, provider-agnostic shared knowledge layer accessible to any AI assistant or human contributor.
- Decision: Created `knowledge/` with four canonical files (README, ASSISTANT_BOOTSTRAP_PROMPT, PROJECT_KNOWLEDGE, DECISIONS). Provider-specific configs become thin behavioral wrappers; all project facts live exclusively in `knowledge/`. `.codex/` is retained for Codex-specific operational context and the append-only SESSION_LOG.
- Impact/Tradeoffs: Better portability, transparency, and human readability; requires discipline to keep project facts out of provider-specific configs and to maintain the data policy (no secrets, no local paths in `knowledge/`).
