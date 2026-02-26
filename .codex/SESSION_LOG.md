# Session Log (append-only)

Regola: questo file e' solo append. Non inserire mai segreti (usare placeholder tipo `<WIFI_PASSWORD>`).

## Entry Template
### YYYY-MM-DD HH:MM (TZ)
- Obiettivo:
- Contesto iniziale:
- Modifiche fatte:
  - `file/percorso`
- Errori incontrati:
  - Sintomo:
  - Causa radice:
  - Fix applicato:
- Verifiche eseguite:
  - Comando:
  - Esito:
- Rischi residui / follow-up:
- Note di prevenzione per prossima sessione:

### 2026-02-26 19:49 (local)
- Obiettivo: stabilizzare workflow repo + memoria operativa + igiene segreti.
- Contesto iniziale: progetto ESPHome con `s3-synthalia.yaml` e segreti locali in `secrets.yaml`.
- Modifiche fatte:
  - `.codex/MEMORY.md`
  - `.codex/SESSION_LOG.md`
  - `.codex/README.md`
  - `.gitignore`
- Errori incontrati:
  - Sintomo: `esphome` non trovato come comando diretto.
  - Causa radice: bin utente Python non presente nel `PATH`.
  - Fix applicato: standardizzato uso `python3 -m esphome`.
- Verifiche eseguite:
  - Comando: `git check-ignore -v secrets.yaml`
  - Esito: `secrets.yaml` ignorato correttamente.
  - Comando: scansione pattern sensibili su `.codex/*`
  - Esito: nessun valore sensibile rilevato.
- Rischi residui / follow-up:
  - Se in futuro viene introdotto `config.h`, mantenere solo template versionato e file locale ignorato.
- Note di prevenzione per prossima sessione:
  - Leggere `MEMORY.md` + ultime 2 entry prima di toccare firmware/config.
