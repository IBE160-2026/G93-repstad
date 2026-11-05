# Tilbakemelding product brief

## 2026-11-05 kl. 10:26 — Syvert Moltu Repstad

### Oppgave
Hente siste endringer fra `origin/main` (som faglærer ba om) og lese tilbakemeldingen på product brief.

### Plan
- Kontrollere repo, gren og rent arbeidsområde, deretter `git pull --ff-only origin main`.
- Lese `tilbakemelding-product-brief.md` og hente ut det gruppen må gjøre videre.

### Resultat
- Pull: `main` ble spolt fram fra `c598365` til `ea84706`. Nye filer: `CLAUDE.md`, `.claude/skills/sesjonslogg/SKILL.md` og tilbakemeldingen på product brief.
- Tilbakemeldingen (faglærer, 2026-10-06): «Godt utgangspunkt med justeringer», vurdert som *enkel* og gjennomførbar. Risiko gjelder testbarhet, kjørbarhet for sensor og kostnad for AI-tjenesten.
- Ingen endringer i briefen ennå.

### Åpne punkter
- Gjøre suksesskriteriene konkrete: antall fiktive CV-er/annonser, sjekkliste per eksempel og hva som er godkjent.
- Avklare oppfølgingsspørsmålene: inn i MVP (når/hvordan svaret brukes) eller flytt til utvidelse.
- Beskrive hvordan koblinger vises: hvert annonsekrav markert «dekket» / «ikke oppgitt» / «mangler», med henvisning til CV-linjen.
- Planlegge én eller to utvidelser, f.eks. filopplasting (PDF/DOCX) eller flere søknadsversjoner i økten.
- Planlegge demomodus med lagrede svar når API-nøkkel mangler, og legge ved fiktive eksempel-CV-er og annonser.
- Velge AI-tjeneste (lav kostnad/gratisnivå), bruke mock-svar under utvikling og beskrive personvernvalget.
- Skissere hvordan koblinger, mangler og utkast presenteres i grensesnittet.
- Repo-plan: testdata i egen mappe, API-nøkkel i `.env` som ikke committes.
- Oppdatere `brief.md` i repoet med endringene, og gå videre til PRD.
