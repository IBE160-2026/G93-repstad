# Spine Pair Review – AI CV & Job Application Assistant

## Overall verdict

Spineparet er en brukbar kontrakt for arkitektur og stories. Begge brukerreisene er speilet med navngitt protagonist, nummererte steg, høydepunkt og feilvei. Alle fargetokener har hex og kontrastverdier, og FR-1–FR-22 og NFR-19–22 er sporet til konkrete komponenter og tilstander uten at noe motsier PRD-ens ikke-mål. De største hullene gjelder oppførsel ved samtidige handlinger og ved bytte av testkombinasjon i demomodus. Begge vil gi tvetydige akseptansekriterier i stories. I tillegg er noen komponent- og knappenavn ikke like i de to spinene, og FR-15 er formulert litt annerledes enn i PRD-en.

## 1. Flow coverage – strong

Sjekket: kildene i frontmatter (PRD, brief, tilbakemelding) → UJ-1 og UJ-2. Begge har en Key Flow med navngitt protagonist (Emma, Ingrid), nummererte steg, merket **Høydepunkt** og feil- eller grensetilfeller (UJ-1: for kort input S0a og tidsavbrudd E1; UJ-2: ugyldig nøkkel E2). Rekkefølgen og innholdet følger PRD §2.3. UJ-1 steg 4–5 (ny analyse, utkast beholdes og merkes) og UJ-2 steg 2–5 (banner, T1, lagrede svar med metadata, T3/T5/T6) er dekket. UJ-2 steg 6 (automatiske tester) og «uten nett» ligger utenfor grensesnittet og er med rette utelatt. Alle FR-1–FR-22 og NFR-19–22 har en rad i «Sporbarhet til PRD».

### Findings

Ingen.

## 2. Token completeness – adequate

Sjekket: alle 33 fargetokener har hex. Bare lyst tema er med, og det er en bevisst beslutning, så det mangler ingen mørke par. Typografi (9 roller), `rounded` (4), `spacing` (10) og 24 komponenttokener er kontrollert. Alle `{…}`-referanser i prosa og komponenter løses, også `{components.focus-indicator}` i EXPERIENCE.md. Kontrast er oppgitt for alle tekstpar på statusflater, varsler og deaktiverte knapper (≥ 6,1:1) og for feltkanten (3,1:1), og alt er innenfor NFR-20.

### Findings

- **medium** Flere synlige komponenter er beskrevet bare i prosa uten tokens, så utviklere må gjette verdiene: «Kopiert ✓»-tilstanden («grønn variant» med `status-covered-bg` og `success-border`, men ingen forgrunnsfarge), metadatalinjen («grå boks»), statusforklaringen, lasteindikatoren (størrelse og strektykkelse), tegntelleren over grensen («blir rød», uten token), toppteksten og dialogskyggen (`0 12px 40px rgba(0,0,0,.3)`, bare i prosa) (DESIGN.md → Components, Elevation & Depth; EXPERIENCE.md → Component Patterns, Inndatafelt). *Fix:* Legg til komponenttokener for `button-copied`, `metadata-line`, `status-legend`, `spinner`, `char-counter-over` og `app-header`, og legg skyggen inn i `dialog`.
- **low** Søknadsutkastet har min. 170 px i prosa, men det finnes bare `input-field.minHeight: 150px`. Det er heller ikke sagt om CV- og annonsefeltene bruker 150 px (DESIGN.md → Components, «Søknadsutkast»). *Fix:* Lag en egen token, for eksempel `draft-field.minHeight: 170px`.
- **low** Kontrast er ikke oppgitt for noen kombinasjoner som bærer innhold: `primary` som tekst på `surface` (sekundærknapper), `status-not-stated` som advarselstekst på `surface` (⚠ i kildekolonnen) og `text-muted` på `surface`. Den stiplede kanten på skrivebeskyttede felt (`field-border` mot `table-header`) ligger på cirka 2,8:1, under 3:1 (DESIGN.md → frontmatter `colors`, `input-field-readonly`). *Fix:* Skriv inn verdiene som kommentarer, og vurder en mørkere stiplet kant eller bekreft at kanten mot den hvite kortflaten (3,1:1) er den som gjelder.

## 3. Component coverage – adequate

Sjekket: DESIGN.md → Components har 16 komponenter, EXPERIENCE.md → Component Patterns har 18 rader. Disse har både visuell spesifikasjon og oppførselsregler: Inndatafelt, Personvernboks, Lasteindikator, Demobanner, Statusforklaring, Metadatalinje, Kravtabell, Forslagskort, Søknadsutkast, Varselboks og Dialog. Oppførselsreglene er konkrete, ikke bare ett ord.

### Findings

- **medium** Knappevariant mangler for flere knapper. DESIGN.md nevner primær bare generelt og plasserer bare «Generer nytt søknadsutkast», «Prøv igjen», «Gå til demomodus», «Behold mitt utkast» og «Lukk». Mockupene bruker primær for «Analyser»/«Analyser på nytt», «Kopier søknadsutkast», «Vis analyse» og «Erstatt», men det står ikke i spinen. Spinen avgjør ved konflikt, så en story kan ikke lese dette ut (DESIGN.md → Components, «Knapper»; mockups/key-resultater.html, key-demomodus.html). *Fix:* Legg inn en tabell over alle knapper med variant og seksjon.
- **medium** Toppteksten (appnavn og ingress) står i IA, men har ingen rad i DESIGN → Components og ingen i Component Patterns. Typografitabellen sier at appnavnet skal være i `primary`, og mockupene viser det slik (`.brand` er #1D4ED8). Det motsier Colors («primær bare til …», toppteksten er ikke nevnt) og Do's and Don'ts («Bruk blått til dekor eller overskrifter») (DESIGN.md → Typography, Colors, Do's and Don'ts). *Fix:* Bestem fargen på appnavnet og legg til en rad for Topptekst. Velges `primary`, må toppteksten tas med som unntak i Colors og Do's.
- **medium** Statuslinjen som melder at analysen er ferdig eller oppdatert, er en komponent i begge spinene, men mangler både visuell spesifikasjon og fast tekst. Den kalles også ulike ting: «Analysen er ferdig» (Accessibility Floor), «analysen er oppdatert» (Interaction Primitives, Rulling) og «Statusen «analysen er oppdatert»» (Merknader til arkitektur). Den står ikke i «Faste tekster» (EXPERIENCE.md, linje 152, 161, 249). *Fix:* Lag én rad «Statuslinje» i begge spinene og én fast tekst for den.
- **low** Statusmerke, Seksjonskort og Fokusindikator har bare visuell spesifikasjon. Oppførselen deres ligger andre steder (Kravtabell, IA: «Seksjon 2–4 vises først etter første analyse», Accessibility Floor), noe som er greit, men det er ikke krysshenvist (EXPERIENCE.md → Component Patterns). *Fix:* Legg til korte rader som peker dit regelen står, eller skriv i innledningen at reglene ligger der.

## 4. State coverage – adequate

Sjekket: overflatene i IA (demobanner, seksjon 1 i vanlig modus og demomodus, seksjon 2, 3 og 4, dialog). Disse er dekket: tom/første besøk (S0, M0), feltfeil (S0a), lasting (S1, generering i seksjon 4), resultater (S2, S3, S4, M1), AI-feil (E1 med fire feiltyper, også i seksjon 4), ugyldig nøkkel (E2), nettverksfeil (E1-tabellen), tomme grupper, ingen forslag, ubekreftet kildehenvisning, kopiering lyktes eller feilet, fokus og omlasting (FR-20).

### Findings

- **high** Bytte av testkombinasjon i demomodus er tvetydig. M2 og UJ-2 steg 5 sier at alt byttes når en annen T *velges*, og at dialog D kommer først hvis utkastet er redigert. Component Patterns sier at valg bare fyller de låste feltene, og at resultatene vises med «Vis analyse». Accessibility Floor gjør listen til en radiogruppe med piltaster, og i en standard radiogruppe følger valget fokus. Hvert piltastetrykk vil da kunne bytte alle resultater eller åpne dialogen. Det er heller ikke sagt hva «Vis analyse» gjør for samme T etter at utkastet er redigert (EXPERIENCE.md, linje 120–121, 143, 166, 207; wireframes/flow-hovedside: «Velg annen T: alle resultater byttes ut»). *Fix:* Bestem én utløser. Anbefalt: valget fyller bare feltene, og byttet med eventuell dialog D skjer først på «Vis analyse». Skriv inn hva som skjer ved «Vis analyse» på samme T, og oppdater M2, UJ-2 steg 5 og flytskissen.
- **high** Samtidige handlinger er ikke avklart. Interaction Primitives sier at «de samme knappene» er låst mens et kall pågår. Det sier ikke om «Analyser på nytt» kan startes mens et nytt søknadsutkast genereres, om søknadsutkastet kan redigeres under genereringen, eller hva som skjer om en ny analyse blir ferdig (og setter merket) mens genereringen pågår. FR-11 sier «basert på siste analyse» og at et redigert utkast ikke erstattes uten bekreftelse. Redigering under generering vil omgå dialogen (EXPERIENCE.md, linje 117, 150). *Fix:* Lås søknadsutkastet og den andre AI-handlingen mens et kall pågår (eller definer en kø), og skriv regelen i Interaction Primitives og i rad S1/S4.
- **medium** Under S1 står det «Feltene kan leses, men de sendte tekstene er det som analyseres». Det er uklart om feltene er skrivebeskyttet eller kan endres, og om «Prøv igjen» i E1 sender den forrige teksten eller teksten som står i feltene nå (EXPERIENCE.md, linje 132, 137). *Fix:* Skriv «Feltene er skrivebeskyttet mens analysen pågår» (eller motsatt), og at «Prøv igjen» sender innholdet i feltene nå, etter ny lengdekontroll.
- **medium** Ugyldig API-nøkkel ved «Generer nytt søknadsutkast» er ikke dekket. Feilmeldingstabellen gir bare «årsak som over» med [Prøv igjen], mens FR-18 krever tilbud om demomodus når nøkkelen avvises (EXPERIENCE.md, linje 97; State Patterns E2 gjelder bare seksjon 1). *Fix:* Skriv at E2 også kan vises i seksjon 4, med «Gå til demomodus» og «Lukk».
- **medium** Fokus etter første analyse er ikke bestemt. Siden ruller til «2 Kravanalyse», men fokus blir stående på knappen i seksjon 1. For tastaturbrukere og skjermlesere (NFR-20) passer ikke da rulleposisjonen og fokus sammen (EXPERIENCE.md → Interaction Primitives, Rulling; Accessibility Floor). *Fix:* Flytt fokus til overskriften «2 Kravanalyse» (`tabindex="-1"`) etter første analyse, og la fokus bli stående ved ny analyse.
- **low** Små grensetilfeller er ikke beskrevet: (a) E2 → «Gå til demomodus» forkaster eventuelle resultater og et redigert utkast uten varsel. (b) Det står ikke hva som skjer hvis personvernbekreftelsen fjernes etter første analyse. (c) Det står ikke om et felt med bare mellomrom regnes som «har tekst», eller om tegntelleren teller med eller uten mellomrom i start og slutt (FR-2 trimmer). (d) Det står ikke hva som vises hvis begge gruppene er tomme (ingen annonsekrav funnet) (EXPERIENCE.md → State Patterns, Component Patterns). *Fix:* Én linje for hvert tilfelle i State Patterns.

## 5. Visual reference coverage – adequate

Sjekket: `mockups/` (key-start, key-lasting-og-feil, key-resultater, key-demomodus), `wireframes/` (ia-hovedside, flow-hovedside), `imports/` (tom) og `.working/directions-1.html`. Ingen fil er foreldreløs. Alle fire mockups og begge skissene er lenket fra EXPERIENCE.md, og directions-1 er lenket fra DESIGN.md. Begge spinene sier at spinen gjelder ved konflikt.

### Findings

- **low** DESIGN.md lenker bare til mappen `mockups/` og ikke til bestemte filer ved relevante seksjoner (Components, Colors) (DESIGN.md, linje 208). *Fix:* Lenk for eksempel key-resultater ved Kravtabell, Forslagskort og Dialog, og key-demomodus ved Demobanner og Testkombinasjon.
- **low** Hver mockup er lenket bare ved én tilstand, selv om den viser flere: key-start viser også S0a, key-lasting-og-feil viser også E1 og E2, og key-resultater viser også D (EXPERIENCE.md → State Patterns). *Fix:* Legg til lenker i radene S0a, E1, E2 og D.
- **low** Skissene og mockupene avviker fra spinene på noen punkter (spinene gjelder, men det kan forvirre). (a) ia-hovedside har dialogtittelen «Erstatte det redigerte søknadsutkastet?» og rekkefølgen [Erstatt] [Behold mitt utkast], mens spinen har «Erstatte søknadsutkastet ditt?» og ghost-knappen først. (b) ia-hovedside viser merket «Basert på forrige analyse (ved ny analyse)» i demomodus, der ny analyse ikke finnes. (c) flow-hovedside viser E2 uten «Lukk». (d) key-lasting-og-feil sier at tidligere resultater blir stående, men viser «Analyser» og ikke «Analyser på nytt». (e) Forslagskortet med «Fremhev» i key-resultater og key-demomodus har teksten «Flytt det til erfaring …». *Fix:* Rett tekstene i skissene og mockupene, eller skriv avvikene i en merknad.

## 6. Bloat & overspecification – strong

Sjekket: EXPERIENCE.md er saklig og bruker tabeller der det passer. «Faste tekster» og feilmeldingstabellen er direkte nyttige for stories. «Sporbarhet til PRD» gjentar bare kravnavnene og brukes som sjekkliste. Ingen persona eller FR-tekst er kopiert inn. DESIGN.md holder prosaen kort og knyttet til beslutninger.

### Findings

- **low** Noen pikselverdier i prosa og komponenter ligger utenfor avstandsskalaen: `padding: '{spacing.5} 22px'`, 18 px mellom feltene, `9px 16px` på knapper og 26 px stegnummer (DESIGN.md, linje 113–134, 255). *Fix:* Bruk skalaverdier (for eksempel `{spacing.5} {spacing.6}`, `{spacing.4}`), eller legg dem inn som navngitte tokener.

## 7. Inheritance discipline – adequate

Sjekket: de tre `sources` løses til eksisterende filer. UJ-navnene er ordrett fra PRD §2.3. Glossarbegrepene (annonsekrav, kravtype, skal-krav, ønsket kvalifikasjon, dekket / ikke oppgitt / mangler, kildehenvisning, kravanalyse, CV-forbedringsforslag, søknadsutkast, «Basert på forrige analyse», demomodus, vanlig modus, lagret svar, testkombinasjon, fasit, AI-tjeneste, API-nøkkel) brukes riktig. Ingen tekst lover jobb, gir match-score, kaller bekreftelsen «samtykke» eller påstår GDPR- eller WCAG-samsvar (§6, NFR-4, NFR-20).

### Findings

- **medium** FR-15 sier at «ny analyse … er deaktivert, med en tydelig forklaring», og at automatiske tester skal verifisere at den er deaktivert. Spinen *erstatter* i stedet «Analyser på nytt» med «Vis analyse» og forklarer en knapp som ikke vises. En story eller test som bygger på PRD-en, vil lete etter en deaktivert knapp (EXPERIENCE.md, linje 122; mockups/key-demomodus.html). *Fix:* Vis «Analyser på nytt» som deaktivert ved siden av «Vis analyse», eller skriv i Sporbarhet hvordan FR-15 tolkes («ny analyse er utilgjengelig: knappen finnes ikke, med forklaring»), slik at testen kan lages ut fra det.
- **medium** Komponentnavnene er ikke like i de to spinene: «Dialog» (DESIGN) / «Bekreftelsesdialog» (Component Patterns) / «D Dialog» (State Patterns), «Testkombinasjon» (DESIGN) / «Liste over testkombinasjoner» (EXPERIENCE), «Merket «Basert på forrige analyse»» / `draft-tag`, og «Knapper» (DESIGN) / «Analyser-knapp», «Kopier søknadsutkast», «Generer nytt søknadsutkast», «Vis analyse» (EXPERIENCE). Stories og komponentnavn i koden vil spre seg (DESIGN.md → Components; EXPERIENCE.md → Component Patterns). *Fix:* Velg ett navn per komponent, gjerne med token-id i parentes, og bruk det i begge filene.
- **low** PRD §3 sier at forklarende tekst skal bruke «stillingsannonse» om selve annonsen. Flere faste tekster bruker «annonsen» («Analyserer CV-en mot annonsen», «Annonsen har ingen skal-krav», «Ingen CV-forbedringsforslag for denne annonsen»), og statusforklaringen bruker «CV-en» der glossaret har «CV-teksten» (EXPERIENCE.md → Faste tekster). *Fix:* Enten skriv «stillingsannonsen» i grensesnittet, eller noter i Voice and Tone at «annonsen» er godkjent kortform i UI-tekst.
- **low** Statusforklaringen for «? Ikke oppgitt» («CV-en sier ingenting om dette …») passer ikke for rader som har fått statusen fordi kildehenvisningen ikke kunne bekreftes (FR-6). Formuleringen «har du kompetansen, kan du legge den til» er i tråd med briefen, men ligger nær grensen i §6 («heller ikke som forslag til hva brukeren «kunne ha»»). Den må forbli generell og aldri bli et forslag per annonsekrav (EXPERIENCE.md, linje 74). *Fix:* Skriv i Component Patterns at forklaringen er fast tekst og ikke genereres per krav. Vurder «CV-teksten avgjør ikke om kravet er oppfylt» i tråd med glossaret.

## 8. Shape fit – strong

Sjekket: DESIGN.md har alle åtte kanoniske seksjoner i riktig rekkefølge. EXPERIENCE.md har alle obligatoriske standardseksjoner (Foundation, Information Architecture, Voice and Tone, Component Patterns, State Patterns, Interaction Primitives, Accessibility Floor, Key Flows). Responsive & Platform er med fordi NFR-21 og breddegrensen gjør den aktuell, og Inspiration & Anti-patterns er med fordi memlog og PRD §6 nevner forkastede mønstre. Rekkefølgen følger eksempelet. De to egne seksjonene, «Sporbarhet til PRD» og «Merknader til arkitektur», har verdi for de som bruker dokumentet videre.

### Findings

Ingen.

## Mechanical notes

- **Frontmatter:** begge spinene har `name`, `status: draft`, `created`, `updated` og tre `sources`, og alle sources løses. DESIGN.md har også `description`. Statusen må settes til `final` etter godkjenning.
- **Token-referanser:** alle `{colors.*}`, `{typography.*}`, `{rounded.*}`, `{spacing.*}` og `{components.focus-indicator}` løses. `danger` og `status-missing` har samme hex (#991B1B). Det er bevisst og forklart.
- **Navnekonflikter:** se kategori 3 og 7. Statuslinjen har tre ulike tekster («Analysen er ferdig» / «analysen er oppdatert»). Dialogtittelen er ulik i skisse og spine. Fargen på appnavnet motsier Do's and Don'ts.
- **Krysshenvisninger:** ankeret `#sporbarhet-til-prd` løses. Alle relative lenker til mockups, wireframes og `.working/directions-1.html` peker på eksisterende filer.
- **Mermaid:** brukes ikke.
- **Språk:** bokmål, med kanoniske BMAD-seksjonsnavn på engelsk. Det er bevisst og ikke et funn.
