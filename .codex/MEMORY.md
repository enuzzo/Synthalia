# Project Memory (Synthalia)

## Prime direttive
- Non scrivere mai segreti in chiaro in file versionati, output o commit message.
- Prima di modifiche firmware, validare sempre con `python3 -m esphome config s3-synthalia.yaml`.
- Per OTA/log usare device esplicito (`--device <ip|hostname>`), non assumere auto-discovery.
- Preferire modifiche minime e verificabili, con rollback semplice.
- Aggiornare questa memoria solo con regole stabili e riusabili.

## Preferenze di lavoro
- Risposte operative, brevi, in italiano.
- Prima sicurezza/coerenza, poi ottimizzazioni.
- Quando possibile: patch piccole + test immediato OTA/log.
- Evitare refactor ampi senza richiesta esplicita.

## Decisioni tecniche consolidate
- Stack: ESPHome su `esp32-s3-devkitc-1` (framework Arduino).
- Config principale: `s3-synthalia.yaml`.
- Segreti runtime: `secrets.yaml` richiamato con `!secret`.
- Comandi standard:
  - Validazione: `python3 -m esphome config s3-synthalia.yaml`
  - Build+OTA: `python3 -m esphome run s3-synthalia.yaml --device <IP>`
  - Log live: `python3 -m esphome logs s3-synthalia.yaml --device <IP>`

## Sicurezza e segreti
- I segreti vivono in `secrets.yaml` (file locale non versionato).
- `secrets.yaml` è escluso da git tramite `.gitignore`.
- I file versionati devono contenere solo riferimenti (`!secret ...`), mai valori sensibili.
- Se in futuro compare `config.h`, mantenerlo locale ignorato e usare template pulito versionato (es. `config.example.h`).

## Gotcha ricorrenti
- `esphome` potrebbe non essere nel `PATH`: usare `python3 -m esphome`.
- `external_components` da GitHub richiede rete attiva (altrimenti validazione fallisce).  
- Dopo rename nodo, primo OTA può richiedere IP diretto invece di hostname.  
- IPOTESI: sensore gesture può sembrare "lento" se filtri/transition sono troppo aggressivi.

## Checklist pre-flight
- [ ] Ho letto questa MEMORY e le ultime 2 entry di `SESSION_LOG.md`.
- [ ] Nessun segreto in chiaro nelle modifiche o nei commenti.
- [ ] `secrets.yaml` resta ignorato e non staged.
- [ ] `python3 -m esphome config s3-synthalia.yaml` passa.
- [ ] Se tocco gesture/luci, faccio test OTA + logs.
- [ ] Aggiorno `SESSION_LOG.md` a fine sessione.
