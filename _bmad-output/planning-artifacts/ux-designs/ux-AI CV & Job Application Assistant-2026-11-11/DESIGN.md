---
name: AI CV & Job Application Assistant
description: Visuell identitet for en norsk webapp på desktop der nyutdannede sammenligner CV-tekst med en stillingsannonse. Retning «Rolig og ryddig» – nummererte seksjonskort på lys bakgrunn, én blå handlingsfarge og tre statusfarger som alltid vises sammen med ikon og tekst.
status: final
created: 2026-11-11
updated: 2026-11-11
sources:
  - "{planning_artifacts}/prds/prd-AI CV & Job Application Assistant-2026-11-05/prd.md"
  - "{planning_artifacts}/briefs/brief-AI CV & Job Application Assistant-2026-09-26/brief.md"
  - "{planning_artifacts}/briefs/brief-AI CV & Job Application Assistant-2026-09-26/tilbakemelding-product-brief.md"
colors:
  # Flater og tekst
  background: '#F5F7FA'
  surface: '#FFFFFF'
  border: '#D9DEE5'
  border-subtle: '#E5E7EB'
  field-border: '#8A94A6'        # 3.1:1 mot hvit – oppfyller 3:1 for UI-komponenter
  field-border-readonly: '#6B7280' # 4.4:1 mot table-header (stiplet kant på låste felt)
  table-header: '#F3F4F6'
  meta-bg: '#F9FAFB'             # text 14.0:1, text-muted 7.2:1
  text: '#1F2937'                # 13.7:1 mot background
  text-muted: '#4B5563'          # 7.0:1 mot background, 7.6:1 mot surface
  # Handling og fokus
  primary: '#1D4ED8'             # som tekst på surface (sekundærknapp, kicker): 6.7:1
  on-primary: '#FFFFFF'          # 6.7:1
  primary-subtle: '#EFF4FF'
  primary-subtle-border: '#C7D7FE'
  focus-ring: '#1D4ED8'
  disabled-bg: '#E5E7EB'
  disabled-text: '#4B5563'       # 6.1:1
  # Status for annonsekrav (tekst på bakgrunn)
  status-covered: '#166534'
  status-covered-bg: '#DCFCE7'   # 6.5:1
  status-not-stated: '#92400E'   # som advarselstekst (⚠) på surface: 7.1:1
  status-not-stated-bg: '#FEF3C7' # 6.4:1
  status-missing: '#991B1B'
  status-missing-bg: '#FEE2E2'   # 6.8:1
  # Varsler og modus
  danger: '#991B1B'              # feltfeiltekst på surface: 8.3:1
  danger-text: '#7F1D1D'         # 9.2:1 mot danger-bg
  danger-bg: '#FEF2F2'
  danger-border: '#FCA5A5'
  demo-text: '#78350F'           # 8.1:1 mot demo-bg
  demo-bg: '#FEF3C7'
  demo-border: '#D97706'
  success-border: '#86EFAC'
typography:
  # Systemfont overalt: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif
  app-title:
    fontFamily: system-ui
    fontSize: 20px
    fontWeight: '700'
    lineHeight: '1.3'
  section-title:
    fontFamily: system-ui
    fontSize: 18px
    fontWeight: '700'
    lineHeight: '1.3'
  group-title:
    fontFamily: system-ui
    fontSize: 15px
    fontWeight: '600'
    lineHeight: '1.4'
  body:
    fontFamily: system-ui
    fontSize: 15px
    fontWeight: '400'
    lineHeight: '1.55'
  field:
    fontFamily: system-ui
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.55'
  label:
    fontFamily: system-ui
    fontSize: 14px
    fontWeight: '600'
    lineHeight: '1.4'
  small:
    fontFamily: system-ui
    fontSize: 13px
    fontWeight: '400'
    lineHeight: '1.45'
  badge:
    fontFamily: system-ui
    fontSize: 13px
    fontWeight: '600'
    lineHeight: '1.4'
  kicker:
    fontFamily: system-ui
    fontSize: 12px
    fontWeight: '700'
    letterSpacing: 0.04em
rounded:
  sm: 4px
  md: 8px
  lg: 10px
  full: 9999px
spacing:
  '1': 4px
  '2': 8px
  '3': 12px
  '4': 16px
  '5': 20px
  '6': 24px
  '7': 28px
  '8': 32px
  page-gutter: 28px
  content-max-width: 1180px
  step-number-size: 26px
components:
  app-header:
    background: '{colors.surface}'
    borderBottom: '1px solid {colors.border}'
    padding: '{spacing.4} {spacing.page-gutter}'
    title: '{typography.app-title} i {colors.text}'
    tagline: '{typography.small} i {colors.text-muted}'
  section-card:
    background: '{colors.surface}'
    border: '1px solid {colors.border}'
    radius: '{rounded.md}'
    padding: '{spacing.5} {spacing.6}'
  step-number:
    background: '{colors.primary}'
    foreground: '{colors.on-primary}'
    size: '{spacing.step-number-size}'
    radius: '{rounded.full}'
  input-field:
    background: '{colors.surface}'
    border: '1px solid {colors.field-border}'
    radius: '{rounded.md}'
    typography: '{typography.field}'
    minHeight: 150px             # CV-tekst og annonsetekst
  input-field-readonly:
    background: '{colors.table-header}'
    border: '1px dashed {colors.field-border-readonly}'
  input-field-error:
    border: '2px solid {colors.danger}'
    message: '{typography.small}, fet, i {colors.danger}'
  draft-field:
    extends: input-field
    minHeight: 170px
  char-counter:
    typography: '{typography.small}'
    foreground: '{colors.text-muted}'
    align: right
  char-counter-over:
    foreground: '{colors.danger}'
    fontWeight: '600'
  button-primary:
    background: '{colors.primary}'
    foreground: '{colors.on-primary}'
    radius: '{rounded.md}'
    padding: '{spacing.2} {spacing.4}'
  button-secondary:
    background: '{colors.surface}'
    foreground: '{colors.primary}'
    border: '1px solid {colors.primary}'
    radius: '{rounded.md}'
  button-ghost:
    background: transparent
    foreground: '{colors.text}'
    border: '1px solid {colors.field-border}'
  button-disabled:
    background: '{colors.disabled-bg}'
    foreground: '{colors.disabled-text}'
    border: '1px solid #D1D5DB'
  button-copied:
    background: '{colors.status-covered-bg}'
    foreground: '{colors.status-covered}'
    border: '1px solid {colors.success-border}'
    content: 'Kopiert ✓'
  spinner:
    size: 16px
    stroke: '3px'
    track: '{colors.primary-subtle-border}'
    indicator: '{colors.primary}'
  status-line:
    typography: '{typography.small}'
    foreground: '{colors.text}'
  status-legend:
    typography: '{typography.small}'
    foreground: '{colors.text}'
    badges: 'status-badge-* uendret'
  metadata-line:
    background: '{colors.meta-bg}'
    border: '1px solid {colors.border-subtle}'
    radius: '{rounded.md}'
    typography: '{typography.small}'
    foreground: '{colors.text-muted}'
  status-badge-covered:
    background: '{colors.status-covered-bg}'
    foreground: '{colors.status-covered}'
    radius: '{rounded.full}'
    content: '✓ Dekket'
  status-badge-not-stated:
    background: '{colors.status-not-stated-bg}'
    foreground: '{colors.status-not-stated}'
    radius: '{rounded.full}'
    content: '? Ikke oppgitt'
  status-badge-missing:
    background: '{colors.status-missing-bg}'
    foreground: '{colors.status-missing}'
    radius: '{rounded.full}'
    content: '✕ Mangler'
  requirement-table:
    headerBackground: '{colors.table-header}'
    border: '1px solid {colors.border-subtle}'
    columns: 'Annonsekrav 34% · Status 16% · Kildehenvisning resten'
  suggestion-card:
    background: '{colors.surface}'
    border: '1px solid {colors.border-subtle}'
    accentBorderLeft: '4px solid {colors.primary}'
    radius: '{rounded.md}'
  privacy-box:
    background: '{colors.primary-subtle}'
    border: '1px solid {colors.primary-subtle-border}'
    radius: '{rounded.md}'
  alert-error:
    background: '{colors.danger-bg}'
    foreground: '{colors.danger-text}'
    border: '1px solid {colors.danger-border}'
    accentBorderLeft: '4px solid {colors.danger}'
    radius: '{rounded.md}'
  demo-banner:
    background: '{colors.demo-bg}'
    foreground: '{colors.demo-text}'
    borderBottom: '2px solid {colors.demo-border}'
  draft-tag:
    background: '{colors.status-not-stated-bg}'
    foreground: '{colors.status-not-stated}'
    radius: '{rounded.full}'
  test-option:
    background: '{colors.surface}'
    border: '1px solid {colors.border}'
    radius: '{rounded.md}'
  test-option-selected:
    background: '{colors.primary-subtle}'
    border: '2px solid {colors.primary}'
  dialog:
    background: '{colors.surface}'
    radius: '{rounded.lg}'
    width: 460px
    shadow: '0 12px 40px rgba(0, 0, 0, 0.3)'
    backdrop: 'rgba(17, 24, 39, 0.45)'
  focus-indicator:
    outline: '2px solid {colors.focus-ring}'
    outlineOffset: 2px
---

# AI CV & Job Application Assistant – DESIGN

Denne fila bestemmer **hvordan appen ser ut**. Oppførsel, tilstander og flyt står i [EXPERIENCE.md](EXPERIENCE.md). Mockupene i [`mockups/`](mockups/) viser tokenene i bruk. Ved konflikt mellom en mockup og denne fila gjelder denne fila.

## Brand & Style

Appen er et arbeidsverktøy for en nyutdannet som skal skrive en jobbsøknad. Uttrykket skal være **rolig, ryddig og troverdig**, omtrent som en moderne nettbank eller offentlig tjeneste. Brukeren skal stole på at det appen sier om CV-en, faktisk står i CV-en. Derfor er designet nøkternt og forutsigbart, uten dekor som konkurrerer med innholdet.

Siden er ett langt dokument delt i fire nummererte seksjonskort (1 Lim inn tekst, 2 Kravanalyse, 3 CV-forbedringsforslag, 4 Søknadsutkast). Nummereringen viser rekkefølgen i arbeidet. Fargen brukes nesten bare til to ting: handlinger (blått) og status for annonsekrav (grønt, gult og rødt). Resten er hvitt, grått og mørk tekst.

Retningen ble valgt fram for alternativet «Dokument og papir» (serif og papirfarger), fordi den er kjent for brukeren, gir tydelige seksjoner og er raskest å bygge med vanlige komponenter. Begge alternativene ligger i [`.working/directions-1.html`](.working/directions-1.html).

## Colors

- **Bakgrunn og flater:** `{colors.background}` (lys grå) bak alt. Seksjonskortene er `{colors.surface}` (hvit) med kant i `{colors.border}`. Skillet mellom bakgrunn og kort er det som deler opp siden.
- **Tekst:** `{colors.text}` for all hovedtekst. `{colors.text-muted}` for hjelpetekst, tegnteller, «Knyttet til»-linjer og forklaringer ved deaktiverte knapper. Ingen tekst er lysere enn `text-muted`.
- **Primær (blå) `{colors.primary}`:** bare til handlinger og «her er du»: primærknapper, sekundærknappenes kant og tekst, stegnumre, venstrekanten på forslagskort, valgt testkombinasjon og fokusring. Appnavnet og overskriftene er i `text`, ikke blått.
- **Status:** tre par med mørk tekst på lys bakgrunn, alle med kontrast fra 6,4:1 og oppover. Statusfargene brukes **aldri** uten ikon og tekst (NFR-20).
  - `status-covered` (grønn): ✓ Dekket
  - `status-not-stated` (gul/brun): ? Ikke oppgitt. Gult signaliserer «se på dette», ikke feil, fordi brukeren kan ha kompetansen uten å ha skrevet den.
  - `status-missing` (rød): ✕ Mangler
- **Feil:** `danger`-fargene brukes bare til varselbokser og feltfeil. Rødt for feil og rødt for «Mangler» har samme tone, men vises i ulike former (varselboks og merke), så de forveksles ikke.
- **Demomodus:** `demo-bg` med `demo-border` gir et gult banner som skiller seg fra alt annet på siden.
- **Merket «Basert på forrige analyse»** bruker de gule `status-not-stated`-fargene. Begge betyr «verdt å se på».

Kontrastverdiene er målt med WCAG-formelen og står som kommentarer i frontmatter. Alle tekstpar er minst 6,1:1. Feltkanten er 3,1:1 mot hvit, og den stiplede kanten på låste felt er 4,4:1 mot grå flate (kravet for UI-komponenter er 3:1). Kontrasten kontrolleres på nytt i den implementerte appen (NFR-20). Appen har bare lyst tema. Mørkt tema er utenfor omfanget.

## Typography

Systemfonten brukes overalt. Den er rask, lesbar og krever ingen nedlasting, så appen virker også uten nett i demomodus (FR-16).

| Rolle | Token | Bruk |
|---|---|---|
| Appnavn | `{typography.app-title}` | «AI CV-assistent» i toppteksten, i `text` |
| Seksjonstittel | `{typography.section-title}` | «1 Lim inn tekst» … «4 Søknadsutkast» |
| Gruppetittel | `{typography.group-title}` | «Skal-krav», «Ønskede kvalifikasjoner» |
| Brødtekst | `{typography.body}` | Forklaringer, forslag, varsler |
| Felt | `{typography.field}` | CV-tekst, annonsetekst, søknadsutkast og tabellceller |
| Etikett | `{typography.label}` | Feltetiketter og knapper |
| Liten | `{typography.small}` | Tegnteller, metadata, «Knyttet til», forklaringer |
| Merke | `{typography.badge}` | Statusmerker og merket på søknadsutkastet |
| Kicker | `{typography.kicker}` | Forslagstype (FREMHEV / OMFORMULER / FLYTT), store bokstaver |

Kildehenvisninger settes i *kursiv* inne i «». Det viser at teksten er sitert ordrett fra CV-en.

## Layout & Spacing

- **Én kolonne.** Innholdet sentreres med maksbredde `{spacing.content-max-width}`. Seksjonskortene har `{spacing.page-gutter}` til siden og `{spacing.5}` mellom seg.
- **Seksjon 1:** CV-tekst og annonsetekst står side om side i to like kolonner med `{spacing.4}` mellomrom. Under dem kommer personvernboksen i full bredde, og deretter en handlingsrad med hjelpetekst til venstre og knappen til høyre.
- **Seksjon 2:** kravtabellene i full bredde, slik at kildehenvisningen får plass.
- **Seksjon 4:** handlingsraden med merke til venstre og knapper til høyre står over tekstfeltet.
- **Demomodus:** listen over testkombinasjoner er et rutenett med tre kolonner og to rader (T1–T6), over feltene.
- Avstandsskalaen bygger på 4 px (`{spacing.1}`–`{spacing.8}`).
- Designet er laget for skjermer fra cirka 1024 px og bredere. Mobiltilpasning er et tilleggsmål (NFR-21) og er ikke designet.

## Elevation & Depth

Siden er flat. Seksjonskortene skilles fra bakgrunnen med farge og kant, ikke med skygge. Bare **dialogen** har skygge (`{components.dialog.shadow}`) og et mørkt slør bak seg (`{components.dialog.backdrop}`), fordi den er det eneste laget over siden.

## Shapes

- `{rounded.md}` (8 px): kort, felt, knapper, varselbokser, personvernboks og testkombinasjoner.
- `{rounded.lg}` (10 px): dialog.
- `{rounded.full}`: statusmerker, merket på søknadsutkastet og stegnumre. Pilleform betyr «status eller etikett», ikke knapp.

## Components

Komponentene kan bygges med vanlig HTML og CSS eller med et standard komponentbibliotek. Valg av teknologi tas i arkitekturfasen. Komponentnavnene er de samme i DESIGN.md og EXPERIENCE.md, med token-id i parentes. Oppførselen står i EXPERIENCE.md → Component Patterns. Mockups: [`key-start`](mockups/key-start.html), [`key-resultater`](mockups/key-resultater.html), [`key-demomodus`](mockups/key-demomodus.html), [`key-lasting-og-feil`](mockups/key-lasting-og-feil.html).

- **Topptekst** (`app-header`): hvit stripe øverst med appnavnet i `{typography.app-title}` og `text`, og én setning i `text-muted` under.
- **Seksjonskort** (`section-card`): hvit flate med kant og 8 px radius. Tittelen har et stegnummer (`step-number`), en blå sirkel med hvitt tall.
- **Inndatafelt** (`input-field`): etikett over feltet og tegnteller (`char-counter`) under, høyrejustert. Over 15 000 tegn bytter telleren til `char-counter-over`. Låst variant (`input-field-readonly`): grå flate med stiplet kant, brukes i demomodus og mens et AI-kall pågår. Feilvariant (`input-field-error`): rød kant på 2 px, med feilmeldingen under.
- **Knapper:** varianten er fast for hver knapp. Det er høyst én primærknapp per seksjon og i dialogen.

  | Knapp | Variant | Sted |
  |---|---|---|
  | Analyser / Analyser på nytt | `button-primary` (deaktivert: `button-disabled`) | Seksjon 1, vanlig modus |
  | Vis analyse | `button-primary` | Seksjon 1, demomodus |
  | Analyser på nytt (demo) | `button-disabled` + forklaring | Seksjon 1, demomodus |
  | Kopier søknadsutkast | `button-primary` → `button-copied` i 2 s | Seksjon 4 |
  | Generer nytt søknadsutkast | `button-secondary` (demo: `button-disabled` + forklaring) | Seksjon 4 |
  | Prøv igjen · Gå til demomodus | `button-secondary` | Varselboks |
  | Lukk | `button-ghost` | Varselboks |
  | Behold mitt utkast | `button-ghost` | Bekreftelsesdialog |
  | Erstatt | `button-primary` | Bekreftelsesdialog |

- **Statusmerke** (`status-badge-*`): pille med ikon og tekst. Teksten brytes ikke.
- **Statusforklaring** (`status-legend`): én linje under tittelen «Kravanalyse» med de tre statusmerkene og en kort fast tekst til hvert.
- **Kravtabell** (`requirement-table`): én tabell per kravtype med kolonnene Annonsekrav, Status og Kildehenvisning fra CV-en. Kolonneoverskriftene har grå bakgrunn, og radene skilles med tynne linjer. Tom kildehenvisning vises som «–». Advarselen om ubekreftet kildehenvisning står i kildekolonnen med «⚠», halvfet og i `status-not-stated`. → [`key-resultater`](mockups/key-resultater.html)
- **Forslagskort** (`suggestion-card`): blå venstrekant, kicker med forslagstype, fet tittel, begrunnelse og «Knyttet til: <annonsekrav>» i liten, dempet tekst.
- **Søknadsutkast** (`draft-field`): stort tekstfelt med minst 170 px høyde. Merket «Basert på forrige analyse» (`draft-tag`) står til venstre i handlingsraden over feltet.
- **Personvernboks** (`privacy-box`): lyseblå boks med fet innledning og avkrysningsboks. Den avkryssede boksen er blå med hvit hake. → [`key-start`](mockups/key-start.html)
- **Varselboks** (`alert-error`): rød venstrekant, fet første setning og knapper under teksten. → [`key-lasting-og-feil`](mockups/key-lasting-og-feil.html)
- **Lasteindikator** (`spinner`) og **statuslinje** (`status-line`): roterende ring foran statusteksten. Tekstene og oppførselen står i EXPERIENCE.md.
- **Demobanner** (`demo-banner`): helt øverst, over toppteksten, i full bredde, med «Demomodus» i fet skrift. → [`key-demomodus`](mockups/key-demomodus.html)
- **Testkombinasjonsliste** (`test-option`, valgt: `test-option-selected`): rutenett med 3 × 2 radioalternativer, hvert med fet tittel («T1 – God match») og beskrivelse under. Valgt alternativ har blå kant på 2 px og lyseblå flate.
- **Metadatalinje** (`metadata-line`): grå boks øverst i Kravanalyse i demomodus, som starter med «Lagret svar, ikke fasit.» i fet skrift.
- **Bekreftelsesdialog** (`dialog`): 460 px bred, med tittel, forklaring og høyrejustert knapperad (ghost først, primær sist). → [`key-resultater`](mockups/key-resultater.html)
- **Fokusindikator** (`focus-indicator`): blå ramme på 2 px med 2 px avstand rundt alle elementer som kan få fokus.

## Do's and Don'ts

| Gjør | Ikke gjør |
|---|---|
| Vis status med ikon, tekst **og** farge | Bruk bare farge, eller bare et ikon, for å vise status |
| Bruk blått bare til handlinger, stegnumre og valgt tilstand | Bruk blått til dekor, appnavn eller overskrifter |
| Sett kildehenvisninger ordrett i «» og kursiv | Forkort, oversett eller omskriv en kildehenvisning |
| Bruk høyst én primærknapp per seksjon | To fylte blå knapper ved siden av hverandre |
| Vis grunnen ved siden av en deaktivert knapp | Deaktiver uten å forklare hvorfor |
| La demobanneret stå synlig hele tiden i demomodus | Skjul eller lukk demobanneret |
| Hold siden flat. Bare dialogen har skygge | Legg skygger på kort for å skape hierarki |
| Mål kontrasten på nytt i den implementerte appen | Påstå samsvar med WCAG 2.1 AA uten kontroll |
| Vis status per annonsekrav, uten samlet poengsum, prosent eller fremdriftsmåler | Lag en «match-score» eller en opptelling av dekkede krav mot totalen |
