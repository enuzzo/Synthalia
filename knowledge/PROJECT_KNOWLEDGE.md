# Synthalia — Project Knowledge

Stable technical context for all assistants. Updated only for verified, reusable facts.

## Repository Layout

- `s3-synthalia.yaml`: entire ESPHome firmware (~1000 lines). Single source for all firmware logic.
- `secrets.yaml`: runtime credentials (git-ignored, never committed).
- `knowledge/`: shared cross-provider knowledge (public, versioned).
- `.codex/`: operational memory and session log — see `.codex/README.md`.
- `assets/`: concept renders and visual references.

## Core Stack

- Platform: ESPHome 2025.2.2+ on ESP32-S3 DevKitC-1 (Arduino framework)
- PSRAM: octal mode, 80 MHz
- LEDs: 300× WS2812B, RMT channel 1, GPIO13
- ToF sensor: VL53L1X @ I2C address 0x29, 400 kHz, GPIO4 (SDA) / GPIO5 (SCL)
- Encoder: KY-040, GPIO11 (A), GPIO12 (B), GPIO10 (button, INPUT_PULLUP, inverted)
- External component: `github://soldierkam/vl53l1x_sensor` (fetched at build time)

## Build Commands

```bash
# Validate config (run before every flash)
python3 -m esphome config s3-synthalia.yaml

# Build and flash over the air
python3 -m esphome run s3-synthalia.yaml --device <DEVICE_IP>

# Stream live logs
python3 -m esphome logs s3-synthalia.yaml --device <DEVICE_IP>
```

## Configuration Boundaries

- Runtime secrets stay only in local `secrets.yaml`.
- Versioned YAML references secrets via `!secret <key>` — never inline values.
- If `config.h` is introduced: keep a versioned template (`config.example.h`) and ignore the real file.

## Operating Modes

Mode is stored in `globals.current_mode` (int):

| Value | Name | Encoder / Hand Action |
|---|---|---|
| 0 | DIM | Brightness control |
| 1 | COLOR | Hue control |
| 2 | EFFECTS | Cycle effects / gesture controls effect parameter |

Single click: DIM ↔ COLOR. Double click: → EFFECTS. Single click from EFFECTS: → DIM.

## Effects Index (current_effect 0–6)

| ID | Name | Update interval |
|---|---|---|
| 0 | Interactive Candy Cane | 16 ms |
| 1 | Interactive Aurora | 16 ms |
| 2 | Interactive Matrix DNA | 16 ms |
| 3 | Interactive Fire | 30 ms |
| 4 | Interactive Plasma Vortex | 16 ms |
| 5 | Interactive Comet Rain | 16 ms |
| 6 | Interactive Nebula Spark | 22 ms |

3 slots still open (roadmap: 10 effects total).

## Global State Variables

| ID | Type | Role |
|---|---|---|
| `current_mode` | int | Active mode (0/1/2) |
| `current_effect` | int | Active effect index (0–6) |
| `hand_present` | bool | ToF detected a hand in range |
| `hand_position` | float 0.0–1.0 | Smoothed gesture output |
| `local_brightness` | int 0–255 | Stored brightness value |
| `local_hue` | float 0–360 | Stored hue in degrees |
| `knob_is_moving` | bool | Encoder activity flag |
| `gesture_log_tick` | int | Throttle for gesture log output |

## Gesture Smoothing Pipeline

The ToF sensor fires at 33 Hz. `hand_position` arriving at effect lambdas is already pre-smoothed:

1. Hardware sliding-window average (window=3) at sensor level.
2. Dead zone: deltas < 0.3% discarded (anti-tremor).
3. Adaptive alpha: 0.16 (small moves) / 0.22 (large moves).
4. Max-step limiter: ±1.8% per frame.
5. Per-effect position smoothing inside each `addressable_lambda` (alpha 0.03–0.30).

When tuning effects: `hand_position` is already pre-smoothed — additional smoothing should be gentle.

## Architecture Notes

- All 7 effects are `addressable_lambda` blocks inside the `main_strip` light entity.
- Each lambda reads `id(hand_present)` and `id(hand_position)` for gesture response.
- `apply_effect` script centralizes effect activation and is called from encoder and button handlers.
- The `sensor: on_value:` lambda handles all gesture processing and dispatches to the light in DIM/COLOR modes; EFFECTS mode is handled entirely inside each lambda.

## Recurring Gotchas

- `esphome` may not be in PATH — always use `python3 -m esphome`.
- External components from GitHub require network access at build time.
- After a node rename, first OTA may require a direct IP instead of hostname.
- Effects lambdas use `static` local arrays (e.g., `heat[300]`, `drops[6]`): these persist between frames but reset on effect switch.
- The hand release threshold is 78 cm (wider than the active range of 10–70 cm) — this prevents value loss on small hand withdrawals.
