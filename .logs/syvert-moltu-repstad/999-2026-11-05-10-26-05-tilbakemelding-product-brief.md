# Tilbakemelding product brief

## 2026-11-05 kl. 10:26 — Syvert Moltu Repstad

### Oppgave
Hente siste endringer fra `origin/main` (som faglærer ba om), lese tilbakemeldingen på product brief og revidere `brief.md` etter den, med gruppens beslutninger om MVP, testsett og demomodus.

### Plan
- Kontrollere repo, gren og rent arbeidsområde, deretter `git pull --ff-only origin main`.
- Lese `tilbakemelding-product-brief.md` og hente ut det gruppen må gjøre videre.
- Vise forslag til revidert brief i chat, innarbeide brukerens tre justeringer, deretter skrive `brief.md`.
- Kontrollere filen (YAML-frontmatter, åtte seksjoner, ingen duplikater, justeringene), committe briefen og loggene hver for seg og pushe uten force.

### Resultat
- Pull: `main` ble spolt fram fra `c598365` til `ea84706`. Nye filer: `CLAUDE.md`, `.claude/skills/sesjonslogg/SKILL.md` og tilbakemeldingen på product brief.
- Tilbakemeldingen (faglærer, 2026-10-06): «Godt utgangspunkt med justeringer», vurdert som *enkel* og gjennomførbar. Risiko gjelder testbarhet, kjørbarhet for sensor og kostnad for AI-tjenesten.
- `brief.md` revidert (åtte seksjoner og frontmatter beholdt, `updated: 2026-11-05`). Kontrollert og godkjent av brukeren, committet som `be54fba` og pushet til `origin/main` sammen med loggcommitene.
  - Kravanalyse med status dekket / ikke oppgitt / mangler og kildehenvisning; oppfølgingsspørsmål ut av MVP.
  - Testsett: 5 fiktive CV-er, 5 annonser, 5 faste kombinasjoner med fasit, sjekkliste på seks punkter. 80 %-grensen gjelder bare klassifisering av annonsekrav; oppdiktede kvalifikasjoner gir alltid ikke bestått.
  - CV-forslag kreves der fasiten viser reelt forbedringsbehov (ikke fast antall).
  - Demomodus bruker bare forhåndsdefinerte fiktive testkombinasjoner med lagrede svar.
  - Personvern, kostnader, mock-svar, `.env` og prioriterte utvidelser (PDF/DOCX, flere søknadsversjoner) beskrevet.

### Åpne punkter
- Lage de fiktive eksempel-CV-ene (CV1–CV5), annonsene (A1–A5) og fasit for de fem testkombinasjonene.
- Velge AI-tjeneste (lav kostnad/gratisnivå) og dokumentere hvordan den behandler data sendt via API-et.
- Skissere hvordan kravanalyse, forslag og utkast presenteres i grensesnittet.
- Gå videre til PRD med den reviderte briefen som grunnlag.
