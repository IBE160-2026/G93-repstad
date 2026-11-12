# Tilbakemelding på PRD

| | |
|---|---|
| **Gruppe** | G93 – G93-repstad |
| **PRD vurdert** | `_bmad-output/planning-artifacts/prds/prd-AI CV & Job Application Assistant-2026-11-05/prd.md` (status `final`, sist endret 2026-11-05, commit 2e07265) |
| **Dato** | 2026-11-12 |
| **Type** | Formativ tilbakemelding, ikke karakter |

## 1. Samlet inntrykk

Dette er en gjennomarbeidet PRD med en tydelig tese (sporbarhet i stedet for match-score), testbare FR-er og et ærlig skille mellom det som testes automatisk og det som evalueres hos KI-en. Den er et solid grunnlag for UX, arkitektur og epics. Risikoen er at «bestått» i evalueringen ikke er endelig definert, at kjøremodellen for vanlig modus er uklar, og at dokumentet er langt og tungt å hente stories fra.

## 2. Dette fungerer godt

- **Tesen er konkret og målbar.** §1: «Hvert dekkede annonsekrav har en kildehenvisning til CV-teksten som applikasjonen selv kontrollerer». FR-6 gjør dette til en mekanisk kontroll (ordrett treff, mellomrom og linjeskift tolereres), med både rått KI-svar og validert resultat i evalueringen.
- **KI-kontroll, kostnad og testmodus er tatt på alvor.** Demomodus (FR-12–FR-17), mock-data (NFR-6, NFR-9), kostnadsramme på 200 kr (NFR-8) og feilhåndtering (FR-18, FR-19) dekker det emnet spør etter. NFR-9 skiller to nivåer: «Beståtte automatiske tester presenteres aldri som dokumentasjon på at KI-analysen er korrekt».
- **Motmål og ærlighet.** SM-C1–SM-C5 (f.eks. SM-C5: «Resultatet skal ikke se bedre ut ved å velge den beste kjøringen») og §1 («Behovet er en hypotese») viser eierskap. Punktene fra briefen-tilbakemeldingen er fulgt opp.

## 3. Oversikt per dimensjon

| Dimensjon | Vurdering | Kort begrunnelse |
|---|---|---|
| Beslutningsklarhet | god | Valg og avveininger er synlige, men «samlet bestått» (§9 spm. 2–3) og kravtype-terskel (SM-5) er åpne. |
| Substans | sterk | Persona og NFR-er driver faktiske krav; lite pynt. |
| Strategisk sammenheng | sterk | Alle funksjoner tjener sporbarhet uten oppdikting; SM-ene validerer tesen. |
| Testbarhet | god | De fleste FR-er har målbare konsekvenser; «forståelig melding» og «relevant forslag» er ikke operasjonalisert. |
| Scope og avgrensning | god | Tydelige Non-Goals og tre MVP-nivåer, men omfanget av evaluering og dokumentasjon er stort, og kjøremodellen er ikke avgrenset. |
| Brukbarhet for neste fase | god | Glossar og ID-er er konsekvente, men UJ-ene har ufullstendig FR-kobling, og dokumentet er langt. |
| Formtilpasning | sterk | UJ-er, features og NFR-er passer en webapp der sensor også er bruker. |

## 4. Viktigste forbedringer

### 4.1 Bestått-regelen må avgjøres nå
- **Alvorlighet:** høy
- **Hvor:** §9 spm. 2–3, §8 «Øvrige kvalitetsmål», NFR-11 «bestått eller ikke bestått»
- **Problem og hvorfor det betyr noe:** Evalueringen er hjertet i kvalitetssikringen, men PRD-en sier ikke når en kjøring, en testkombinasjon og hele evalueringen er bestått. FR-5 og SM-4 sier heller ikke om status måles på rått KI-svar eller etter appens validering (FR-6 og SM-2 er tydelige på det). Epics og tester for evalueringen kan ikke skrives uten en regel, og regelen bør settes før dere ser resultatene.
- **Forslag:** Lås regelen, for eksempel: «En kjøring er bestått når SM-1 og SM-2 er 0, alle fasit-annonsekrav er funnet (SM-3), status stemmer for minst 80 % av funne annonsekrav målt på rått KI-svar (SM-4), og kravtype stemmer for minst 80 % (SM-5). En testkombinasjon er bestått når alle kjøringer er bestått. Samlet bestått krever T1–T5; T6 rapporteres separat, men SM-1 og SM-2 gjelder.» Flytt spørsmålene fra §9 til beslutninger.

### 4.2 Hvor kjører vanlig modus, og hvem betaler?
- **Alvorlighet:** medium
- **Hvor:** UJ-1 «appen har API-nøkkel (vanlig modus)», NFR-8, NFR-14, NFR-15 «vanlig modus aktiveres med egen nøkkel»
- **Problem og hvorfor det betyr noe:** Emma åpner «webappen i nettleseren» uten egen nøkkel, men appen kan også klones og kjøres lokalt med egen nøkkel. Om dere skal drifte en offentlig versjon, påvirker det arkitekturen (hosting, vern mot misbruk og kostnad, NFR-18) og budsjettet på 200 kr.
- **Forslag:** Legg til en avgrensning, f.eks.: «I MVP kjøres appen lokalt. Vanlig modus krever at den som kjører appen oppgir egen API-nøkkel. Offentlig drift er utenfor scope.» Eller beskriv hva en offentlig versjon må kreve (kostnadstak, rate limit).

### 4.3 Gjør «forståelig» og «relevant» testbart
- **Alvorlighet:** medium
- **Hvor:** FR-2 «forståelig melding», FR-18/FR-19 «forståelig feilmelding», SM-6/FR-8 «relevant og begrunnet»
- **Problem og hvorfor det betyr noe:** Testskriveren og den som evaluerer kan ikke avgjøre når dette er oppfylt.
- **Forslag:** Legg til konsekvenser som: «Feilmeldingen oppgir feiltypen (ugyldig nøkkel, tidsavbrudd, nettverk, kvote eller ufullstendig svar), sier at innholdet er beholdt, og har en knapp for å prøve igjen.» For SM-6: «Forslaget viser til samme annonsekrav som fasiten og bygger på en passasje i CV-teksten.»

### 4.4 Lengde og prioritering for epics
- **Alvorlighet:** medium
- **Hvor:** hele dokumentet (ca. 6 200 ord, 22 FR, 23 NFR, 15 SM, 7 åpne spørsmål); NFR-13 (18 kjøringer)
- **Problem og hvorfor det betyr noe:** Evaluering, fasit for seks kombinasjoner, lagrede svar og versjonering (NFR-12) er mer arbeid enn selve kjerneappen. Stories blir lettere å lage, og risikoen lettere å styre, hvis det er tydelig hva som er app, hva som er leveranse og hva som er prosess.
- **Forslag:** Merk hver NFR som `[app]`, `[leveranse]` eller `[prosess]`, og ta med en kort tabell FR/NFR til epic-kandidat. Behold reduksjonsregelen i NFR-13 (én kjøring per kombinasjon) som uttalt reserveplan.

### 4.5 Rydd bort utkasttekst før «final»
- **Alvorlighet:** lav
- **Hvor:** §2.3 «(FR-numrene settes i seksjon 4)», «Dette skal bli et testbart krav.», «Dette skal knyttes til et testbart akseptansekriterium.»
- **Problem og hvorfor det betyr noe:** Listene «Funksjoner reisen krever» mangler FR-henvisninger, og formuleringene er arbeidsnotater. Status `final` med åpne spørsmål signaliserer mer enn dokumentet holder.
- **Forslag:** Skriv f.eks. «Systemet må avvise for kort input med en forståelig melding. → FR-2, FR-3», og sett status til `draft` til §9 er lukket.

## 5. Mekaniske funn

- ID-er er sammenhengende (UJ-1–2, FR-1–22, NFR-1–23, SM-1–10, SM-C1–C5), og krysshenvisningene jeg stikkprøvde løser seg.
- Glossaret brukes stort sett konsekvent. Små avvik: «funne annonsekrav» (bør være «funnede»), og blanding av «KI-svar» og «AI-tjeneste».
- FR-3, FR-8, FR-9, FR-11 og FR-19 mangler «Realiserer UJ-x», i motsetning til de andre.
- Ingen inline `[ASSUMPTION]`-tagger; §10 lister bare tre bekreftede antakelser. Åpne punkter er merket `[ÅPENT SPØRSMÅL]` og samlet i §9.

## 6. Før dere går videre

**Må avklares før UX, arkitektur og epics:**
- Bestått-regelen og kravtype-terskelen (§9 spm. 1–3, punkt 4.1).
- Kjøremodellen for vanlig modus (punkt 4.2) og budsjettrammen (spm. 4).
- Valg av AI-tjeneste (spm. 5), som gjøres i arkitekturen.

**Kan vente:** lengdegrensene (spm. 6) til testdata og modell finnes, brukerutprøving (spm. 7), tilleggsmålene i §7.3.

**Oppfølging av briefen-tilbakemeldingen: ja.** Suksesskriteriene er konkrete (T1–T6, sjekkliste, terskler), oppfølgingsspørsmål er tatt ut (§6), kildehenvisning og status er synlig i grensesnittet, demomodus er med, og utvidelser er planlagt (§7.4).

## 7. Refleksjonsspørsmål

1. Hvilke deler av PRD-ens tall (300/200/15 000 tegn, 80 %, 200 kr, 60 s) har dere selv begrunnet, og hvilke kom fra KI-forslag? Hvordan vil dere se at de er riktige?
2. PRD-en er lang og detaljert. Hvilke krav ville dere kuttet først hvis tiden ble knapp, og hvordan kan dere sjekke at det ikke svekker tesen om sporbarhet?

_Vurdert mot kvalitetsrubrikken i bmad-prd. Dette er veiledning, ikke sensur._
