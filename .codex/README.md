# .codex usage

Questa cartella contiene memoria operativa di progetto, senza dati sensibili.

## Differenza tra file
- `MEMORY.md`: regole stabili, decisioni consolidate, checklist pre-flight.
- `SESSION_LOG.md`: diario cronologico append-only di sessioni, errori e correzioni.

## Rituale inizio sessione
- Leggi `MEMORY.md`.
- Leggi le ultime 2 entry di `SESSION_LOG.md`.
- Allinea il piano di lavoro a quelle regole prima di toccare codice/config.

## Rituale fine sessione
- Appendi una nuova entry in `SESSION_LOG.md` (obiettivo, errori, fix, verifiche, follow-up).
- Aggiorna `MEMORY.md` solo se emerge una regola stabile e riusabile.
- Mantieni i cambi minimali e verificati.

## Sicurezza (obbligatoria)
- Divieto assoluto di segreti in `.codex/*`.
- Niente password/token/API key in output o commit message.
- I segreti restano in file locali ignorati da git (es. `secrets.yaml`).
