# Synthalia

> **A 5m ESP32-S3 light instrument** for people who say  
> _"it's vibe coded"_ and then still tune timing constants like a maniac.

## What This Is

`Synthalia` is an ESPHome-powered LED project with:

- 🖐️ Hand gesture control (VL53L1X ToF)
- 🎛️ Rotary encoder + push button modes
- 🌈 Smooth dim/color control
- ✨ Interactive effects (Candy Cane, Aurora, Matrix, Fire)
- 📡 OTA update workflow

Yes, the project is vibe coded.  
No, it is not random.  
It is **taste-driven + parameter-disciplined chaos**.

---

## Creative Direction

Built under the watchful eye of an **"humble creative director"** (their words, we respect it), with one non-negotiable rule:

**If it feels clunky, it is wrong.**

---

## Quick Start

```bash
python3 -m esphome config s3-synthalia.yaml
python3 -m esphome run s3-synthalia.yaml --device <DEVICE_IP_OR_HOSTNAME>
python3 -m esphome logs s3-synthalia.yaml --device <DEVICE_IP_OR_HOSTNAME>
```

Example:

```bash
python3 -m esphome run s3-synthalia.yaml --device 192.168.178.151
```

---

## Control Model

- `Single click`: cycle `DIM -> COLOR -> DIM`
- `Double click`: enter `EFFECTS` mode
- `Single click` from effects: exit to `DIM`
- `Encoder`: adjust brightness / hue / effect selection (by mode)
- `Hand`: gesture mapping by active mode

---

## Effects (Current)

1. 🍬 Interactive Candy Cane
2. 🌌 Interactive Aurora
3. 🧬 Interactive Matrix
4. 🔥 Interactive Fire (smooth, hand-aware)

Roadmap target: **10 effects** total.

---

## Repo Hygiene

- Secrets stay in local `secrets.yaml` (ignored by git)
- Never commit keys/passwords/tokens
- Keep OTA + logs reproducible
- Keep commits in English

---

## License

MIT (or choose your preferred license before public launch).
