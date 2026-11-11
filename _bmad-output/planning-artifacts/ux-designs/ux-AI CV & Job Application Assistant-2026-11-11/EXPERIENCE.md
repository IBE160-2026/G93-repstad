---
name: AI CV & Job Application Assistant
status: final
created: 2026-11-11
updated: 2026-11-11
sources:
  - "{planning_artifacts}/prds/prd-AI CV & Job Application Assistant-2026-11-05/prd.md"
  - "{planning_artifacts}/briefs/brief-AI CV & Job Application Assistant-2026-09-26/brief.md"
  - "{planning_artifacts}/briefs/brief-AI CV & Job Application Assistant-2026-09-26/tilbakemelding-product-brief.md"
---

# AI CV & Job Application Assistant – EXPERIENCE

Denne fila beskriver **hvordan appen fungerer**: sideoppbygging, tilstander, oppførsel, tekster og tilgjengelighet. Det visuelle står i [DESIGN.md](DESIGN.md), og token-navn vises som `{path.to.token}`. Begrepene følger ordlisten i PRD §3 nøyaktig. Ved konflikt mellom en mockup eller skisse og denne fila gjelder denne fila.

## Foundation

- **Form:** webapp for nettleser på datamaskin (NFR-21). Hele appen er **én side** med fire seksjoner. Det finnes ingen navigasjon, innlogging eller flere sider.
- **Moduser:** *vanlig modus* (med API-nøkkel) og *demomodus* (uten API-nøkkel). Begge bruker den samme siden. Demomodus endrer innholdet i seksjon 1 og deaktiverer noen handlinger (FR-12–FR-17).
- **Språk:** grensesnitt og resultater på norsk bokmål (NFR-19).
- **UI-system:** ikke bestemt. Rammeverket velges i arkitekturfasen. Designet krever ingenting som et standard komponentbibliotek eller vanlig HTML ikke dekker, og dialogen kan bygges med HTML-elementet `<dialog>`.
- **Visuell identitet:** DESIGN.md, retning «Rolig og ryddig».
- **Rammer:** studentprosjekt med bare fiktive data, men designet for en ekte målgruppe og vurdert av sensor. Ærlighet og sporbarhet veier tyngre enn effekter.

## Information Architecture

Én side, lest ovenfra og ned. Seksjon 2–4 vises først etter første analyse (eller etter «Vis analyse» i demomodus).

| Område | Vanlig modus | Demomodus | Krav |
|---|---|---|---|
| Demobanner | – | Alltid øverst, kan ikke lukkes | FR-13 |
| Topptekst | Appnavn og én setning om hva appen gjør | Samme | – |
| **1 Lim inn tekst** / **1 Velg testkombinasjon** | CV-tekst og annonsetekst side om side med tegnteller · personvernboks med avkrysning · varselboks ved feil · «Analyser» / «Analyser på nytt» | Liste T1–T6 · skrivebeskyttede felt med fiktiv tekst · forklaring med henvisning til README · «Vis analyse» · «Analyser på nytt» deaktivert | FR-1–3, FR-14, FR-17, FR-18, FR-19, FR-22 |
| **2 Kravanalyse** | Statusforklaring · tabell «Skal-krav» · tabell «Ønskede kvalifikasjoner» | Samme, med metadatalinje øverst | FR-4–7, FR-15 |
| **3 CV-forbedringsforslag** | Ett kort per forslag | Samme | FR-8 |
| **4 Søknadsutkast** | Merke ved behov · «Generer nytt søknadsutkast» · «Kopier søknadsutkast» · redigerbart felt | «Generer nytt» deaktivert med forklaring · kopiering og redigering virker | FR-9–11, FR-15 |
| Dialog | «Erstatte søknadsutkastet ditt?» | Samme, ved bytte av testkombinasjon når utkastet er redigert | FR-11 |

Alle krav i PRD-en har en plass på siden, og alle delene av siden hører til UJ-1 (Emma) eller UJ-2 (Ingrid). Se [Sporbarhet til PRD](#sporbarhet-til-prd).

→ Skisser: [`wireframes/ia-hovedside-2026-11-11.excalidraw`](wireframes/ia-hovedside-2026-11-11.excalidraw) (oppbyggingen av siden) og [`wireframes/flow-hovedside-2026-11-11.excalidraw`](wireframes/flow-hovedside-2026-11-11.excalidraw) (flyten mellom tilstandene). Åpnes på excalidraw.com.

## Voice and Tone

Tonen er **rolig, direkte og ærlig**. Appen snakker til brukeren med «du», sier hva som skjer, og lover aldri mer enn den kan holde.

- Bruk ordene fra PRD-ordlisten nøyaktig: *annonsekrav, kravtype, skal-krav, ønsket kvalifikasjon, dekket, ikke oppgitt, mangler, kildehenvisning, kravanalyse, CV-forbedringsforslag, søknadsutkast, demomodus, vanlig modus*.
- Feilmeldinger sier **hva som skjedde**, **hva som er beholdt** og **hva brukeren kan gjøre**.
- Personvernteksten kalles «informasjon» og «bekreftelse», aldri «samtykke». Den påstår ingenting om GDPR (FR-22, NFR-4).
- Appen lover ikke jobb eller intervju og gir ingen samlet vurdering av CV-en (PRD §6).
- Forklarende tekst bruker «stillingsannonsen» og «CV-teksten», som i PRD-ordlisten. Bare toppteksten og plassholderen for CV-tekst bruker den mer personlige formen «CV-en din».

| Gjør | Ikke gjør |
|---|---|
| «CV-teksten er for kort til å analysere. Den må ha minst 300 tegn (nå 142). Ingenting er sendt.» | «Ugyldig input!» |
| «Analysen ble ikke fullført. AI-tjenesten svarte ikke innen ett minutt. Teksten din og eventuelle tidligere resultater er beholdt.» | «Error 504 – timeout» |
| «Jeg har lest informasjonen» | «Jeg samtykker» / «Jeg godtar vilkårene» |
| «CV-teksten sier ingenting som avgjør om kravet er oppfylt – har du kompetansen, kan du legge den til og analysere på nytt» | «Du mangler Power BI» (når CV-teksten bare ikke nevner det) |
| «Lagret svar, ikke fasit.» | «Fasit» / «Riktig svar» |
| «Kontroller alltid innholdet før du bruker det.» | «Søknaden er klar til å sendes!» |

### Faste tekster

| Sted | Tekst |
|---|---|
| Topptekst | «Se hvordan CV-en din møter kravene i en stillingsannonse, og få forslag og et søknadsutkast basert på det som faktisk står i CV-en.» |
| Plassholder CV-tekst | «Lim inn teksten fra CV-en din her.» |
| Plassholder annonsetekst | «Lim inn teksten fra stillingsannonsen her. Den kan være på norsk eller engelsk.» |
| Tegnteller | «{antall} / 15 000 tegn» |
| Personvernboks | «**Før du analyserer:** CV-teksten og annonseteksten sendes til en ekstern AI-tjeneste for å lage analysen. Fjern unødvendige personopplysninger, som telefonnummer, e-postadresse og adresse, før du limer inn. Appen lagrer ikke teksten – alt forsvinner når du lukker eller laster inn siden på nytt.» + ☐ «Jeg har lest informasjonen» |
| Hjelpetekst ved deaktivert «Analyser» | «Lim inn begge tekstene og bekreft informasjonen for å starte analysen.» |
| For kort (FR-2) | «{CV-teksten/Annonseteksten} er for kort til å analysere. Den må ha minst {300/200} tegn (nå {n}). Ingenting er sendt.» |
| For lang (FR-3) | «{CV-teksten/Annonseteksten} er for lang. Kort den ned med {n} tegn (maks 15 000). Ingenting er sendt.» |
| Laster | «Analyserer CV-teksten mot stillingsannonsen. Dette kan ta opptil ett minutt.» / «Genererer nytt søknadsutkast …» |
| Statuslinje etter analyse | «Analysen er ferdig.» (første analyse) / «Analysen er oppdatert. Søknadsutkastet ditt er beholdt.» (ny analyse) / «Nytt søknadsutkast er laget.» |
| Statusforklaring (fast tekst, aldri per krav) | «✓ Dekket – CV-teksten dokumenterer kravet» · «? Ikke oppgitt – CV-teksten sier ingenting som avgjør om kravet er oppfylt – har du kompetansen, kan du legge den til og analysere på nytt» · «✕ Mangler – CV-teksten viser at kravet ikke er oppfylt» |
| Ubekreftet kildehenvisning (FR-6) | «⚠ Kildehenvisningen kunne ikke bekreftes i CV-teksten, så kravet vises ikke som dekket.» |
| Tom gruppe | «Stillingsannonsen har ingen skal-krav.» / «Stillingsannonsen har ingen ønskede kvalifikasjoner.» |
| Ingen annonsekrav funnet | «Fant ingen annonsekrav i annonseteksten. Kontroller at du har limt inn hele stillingsannonsen.» |
| Ingen forslag (FR-8) | «Ingen CV-forbedringsforslag for denne stillingsannonsen. Analysen fant ikke noe i CV-teksten som bør fremheves, omformuleres eller flyttes.» |
| Under søknadsutkastet | «Du kan redigere teksten direkte. Kontroller alltid innholdet før du bruker det.» |
| Kopiert / feil ved kopiering | «Kopiert ✓» / «Kunne ikke kopiere. Marker teksten og kopier den manuelt.» |
| Dialog (FR-11) | Tittel «Erstatte søknadsutkastet ditt?» · «Du har endret søknadsutkastet. Et nytt utkast erstatter teksten din, og endringene dine går tapt.» · [Behold mitt utkast] [Erstatt] |
| Demobanner | «**Demomodus** – du ser lagrede svar for fiktive eksempler. Ingenting sendes til en AI-tjeneste. Vil du analysere egen tekst, trenger du vanlig modus med API-nøkkel (se README).» |
| Låste felt i demo | «🔒 Feltene er låst i demomodus. Demomodus viser bare de forhåndsdefinerte testkombinasjonene. Slik analyserer du egen tekst: se «Vanlig modus» i README.» |
| Deaktivert i demo | Ved «Analyser på nytt» og «Generer nytt søknadsutkast»: «Krever vanlig modus med API-nøkkel.» |
| Metadata i demo | «**Lagret svar, ikke fasit.** T{n} · Kjøring {k} · Modell: {modell} · Promptversjon: {versjon} · Dato: {ÅÅÅÅ-MM-DD}» |

### Feilmeldinger fra AI-tjenesten (FR-18, FR-19)

Første setning er fet. Etter hver melding om analyse i tabellen nedenfor legges setningen «Teksten din og eventuelle tidligere resultater er beholdt.» til.

| Feil | Melding | Knapper |
|---|---|---|
| Tidsavbrudd (60 s, NFR-22) | «**Analysen ble ikke fullført.** AI-tjenesten svarte ikke innen ett minutt.» | Prøv igjen |
| Nettverksfeil | «**Analysen ble ikke fullført.** Appen fikk ikke kontakt med AI-tjenesten. Sjekk nettforbindelsen og prøv igjen.» | Prøv igjen |
| Kvote- eller kostnadsgrense | «**Analysen ble ikke fullført.** AI-tjenesten avviste forespørselen fordi en bruks- eller kostnadsgrense er nådd. Prøv igjen senere.» | Prøv igjen |
| Svar som ikke kan tolkes eller er ufullstendig | «**Analysen ble ikke fullført.** Svaret fra AI-tjenesten var ufullstendig og kan ikke vises.» | Prøv igjen |
| Ugyldig API-nøkkel | «**AI-tjenesten godtok ikke API-nøkkelen.** Sjekk nøkkelen i `.env`-fila (se README). Du kan også gå til demomodus og se lagrede svar for fiktive eksempler – teksten du har limt inn og eventuelle resultater blir da ikke tatt med.» | Gå til demomodus · Lukk |
| Ugyldig API-nøkkel ved nytt søknadsutkast | Samme tekst som over, vist i seksjon 4. Utkastet er beholdt. | Gå til demomodus · Lukk |
| Nytt søknadsutkast feilet | «**Det nye søknadsutkastet ble ikke laget.** Utkastet ditt er beholdt uendret.» + andre setning fra raden for samme feiltype over (for eksempel «AI-tjenesten svarte ikke innen ett minutt.») | Prøv igjen |

## Component Patterns

Her står oppførselen. Det visuelle står i DESIGN.md → Components.

| Komponent | Bruk | Regler for oppførsel |
|---|---|---|
| Topptekst | Øverst | Statisk. Ingen lenker eller handlinger. |
| Inndatafelt (CV-tekst, annonsetekst) | Seksjon 1 | Flerlinjet tekstfelt med synlig etikett. Tegntelleren og lengdekontrollen teller tegn etter at mellomrom i starten og slutten er fjernet (FR-2). Et felt med bare mellomrom regnes som tomt. Telleren oppdateres mens brukeren skriver og blir rød over 15 000. Teksten blir stående etter analysen (FR-1). Lengden kontrolleres når brukeren trykker «Analyser». Ved feil får feltet rød kant og meldingen står rett under. Meldingen forsvinner når feltet endres. Låses under AI-kall (se Interaction Primitives). |
| Personvernboks | Seksjon 1, bare i vanlig modus | Avkrysningen gjelder resten av økten og lagres ikke (FR-22, FR-20). Boksen blir stående synlig etter avkrysning. Fjernes avkrysningen, blir «Analyser» / «Analyser på nytt» deaktivert igjen. Resultatene blir stående. |
| Analyser-knapp | Seksjon 1 | Deaktivert til begge feltene har tekst **og** informasjonen er bekreftet. Mens knappen er deaktivert, står hjelpeteksten «Lim inn begge tekstene …» ved siden av. Heter «Analyser» før første analyse og «Analyser på nytt» etterpå. Låst mens analysen pågår (FR-1). |
| Lasteindikator | Seksjon 1 / seksjon 4 | Vises bare mens et kall pågår, sammen med statuslinjen. Etter 60 sekunder regnes kallet som tidsavbrudd, og E1 vises (NFR-22). |
| Statuslinje | Seksjon 1 / seksjon 4 | `aria-live="polite"`. Viser lasteteksten mens kallet pågår og deretter den faste teksten for resultatet («Analysen er ferdig.» osv.) til neste handling. |
| Demobanner | Øverst, demomodus | Alltid synlig, kan ikke lukkes, står over toppteksten. Vises også når demomodus er valgt etter E2 (FR-13). |
| Statusforklaring | Seksjon 2 | Fast linje under tittelen. Den forklarer de tre statusene med samme merker som i tabellen. Teksten er fast og genereres aldri per annonsekrav (PRD §6). Den kan ikke klikkes. |
| Statusmerke · Seksjonskort · Fokusindikator | Hele siden | Har ingen egen oppførsel. Regelen for statusmerker står under Kravtabell, regelen om at seksjon 2–4 vises først etter analyse står i Information Architecture, og fokusregler står i Accessibility Floor. |
| Metadatalinje | Seksjon 2, demomodus | Viser kjøringsnummer, modell, promptversjon og dato for den valgte testkombinasjonen og starter alltid med «Lagret svar, ikke fasit.» (FR-15). |
| Kravtabell | Seksjon 2 | To tabeller: «Skal-krav» og «Ønskede kvalifikasjoner» (FR-4). Kravene står i samme rekkefølge som i stillingsannonsen. Hver rad har nøyaktig én status (FR-5). Krav med status «Dekket» vises med kildehenvisningen ordrett, uten forkorting (FR-6). «Ikke oppgitt» og «Mangler» har «–» i kildekolonnen. En gruppe uten krav viser en tom-tekst i stedet for tabell. Ingen sortering, filtrering eller samlet poengsum. |
| Ubekreftet kildehenvisning | Seksjon 2 | Kravet vises med status «Ikke oppgitt» og advarselen i kildekolonnen. Den ugyldige teksten vises aldri (FR-6). Gjelder også lagrede svar (FR-15). |
| Forslagskort | Seksjon 3 | Ett kort per CV-forbedringsforslag: type (Fremhev / Omformuler / Flytt), kort tittel, begrunnelse og «Knyttet til: <annonsekrav>» (FR-8). Kortene kan bare leses. Ved flere tilknyttede krav skilles de med komma. |
| Søknadsutkast | Seksjon 4 | Redigerbart flerlinjet felt (FR-9). Skrivebeskyttet mens et AI-kall pågår. Appen registrerer om brukeren har endret teksten etter at utkastet ble laget («redigert»). Ved ny analyse beholdes utkastet uendret (FR-10). |
| Merke «Basert på forrige analyse» | Seksjon 4, vanlig modus | Vises når en ny analyse er ferdig og et søknadsutkast finnes. Fjernes bare når et nytt søknadsutkast er laget (FR-10, FR-11). Vises aldri i demomodus. |
| Kopier søknadsutkast | Seksjon 4 | Kopierer hele den nåværende teksten, også endringene, med ett klikk. Knappen viser «Kopiert ✓» i cirka 2 sekunder og meldes til skjermleser. Ved feil vises meldingen om manuell kopiering. |
| Generer nytt søknadsutkast | Seksjon 4, vanlig modus | Vises når et utkast finnes. Er utkastet redigert, åpnes dialogen først. Ellers starter genereringen direkte. Knappen blir «Genererer …» og er låst mens genereringen pågår. Lykkes den, byttes teksten og merket fjernes. Feiler den, beholdes utkastet og merket, og en varselboks vises i seksjon 4 (FR-11). Avvises API-nøkkelen, vises E2 i seksjon 4 (FR-18). |
| Bekreftelsesdialog | Over siden | Modal. Fokus starter på «Behold mitt utkast». Esc og klikk utenfor virker som «Behold mitt utkast». Når dialogen lukkes, går fokus tilbake til knappen som åpnet den. Brukes ved «Generer nytt søknadsutkast» og ved «Vis analyse» for en ny testkombinasjon i demomodus når utkastet er redigert. |
| Varselboks | Seksjon 1 (analyse) / seksjon 4 (nytt utkast) | Vises over handlingsraden. Den blir stående til brukeren prøver igjen, lukker den eller starter en ny handling. Inneholder aldri brukerens tekst (FR-21). |
| Testkombinasjonsliste | Seksjon 1, demomodus | Radioknapper T1–T6 med tittel og beskrivelse (FR-14). Ingen er valgt ved oppstart. Valg med klikk, mellomrom eller piltaster fyller **bare** de låste feltene med den fiktive CV-teksten og annonseteksten. Seksjon 2–4 endres ikke før «Vis analyse». |
| Vis analyse | Seksjon 1, demomodus | Aktiv når den valgte testkombinasjonen ikke allerede vises. Bytter seksjon 2–4 til de lagrede svarene for den valgte kombinasjonen med en gang. Det gjøres ingen kall og det er ingen lasting (FR-16). Er søknadsutkastet redigert, åpnes bekreftelsesdialogen først. Velger brukeren «Behold mitt utkast», settes listen og feltene tilbake til kombinasjonen som vises. |
| Deaktivert handling med forklaring | Demomodus | «Analyser på nytt» (ved siden av «Vis analyse») og «Generer nytt søknadsutkast» er synlige men deaktivert, med teksten «Krever vanlig modus med API-nøkkel.» ved siden av (FR-15). |

## State Patterns

Tilstandsnavnene (S0, S1, …) samsvarer med flytskissen.

| Tilstand | Område | Slik vises den |
|---|---|---|
| **S0 Klar** | Vanlig modus, første besøk | Bare seksjon 1. Tomme felt med plassholder og tegnteller «0 / 15 000 tegn». Personvernboksen er ikke krysset av. «Analyser» er deaktivert med hjelpetekst. → [`mockups/key-start.html`](mockups/key-start.html) |
| **S0a Feltfeil** | Seksjon 1 | For kort eller for lang tekst: rød kant på feltet, melding under og fokus flyttet til det første feltet med feil. Ingenting sendes (FR-2, FR-3). Begge feltene kan ha feil samtidig. → [`mockups/key-start.html`](mockups/key-start.html) |
| **S1 Analyserer** | Seksjon 1 | Knappen «Analyserer …» er låst, og statuslinjen viser roterende ring. Alt annet er låst som beskrevet under «Én AI-handling om gangen» i Interaction Primitives. Tidligere resultater i seksjon 2–4 blir stående uendret til det nye svaret er klart. → [`mockups/key-lasting-og-feil.html`](mockups/key-lasting-og-feil.html) |
| **S2 Resultater** | Seksjon 2–4 | Første analyse: kravanalyse, forslag og et nytt søknadsutkast uten merke. Rulling og fokus: se Interaction Primitives. Statuslinjen: «Analysen er ferdig.» |
| **S2a Ingen annonsekrav funnet** | Seksjon 2 | Fast tekst i stedet for tabellene. Seksjon 3 og 4 vises som vanlig. |
| **S3 Ny analyse ferdig** | Seksjon 2–4 | Seksjon 2 og 3 er erstattet. Søknadsutkastet er beholdt med merket «Basert på forrige analyse» (FR-10). Rulling og fokus: se Interaction Primitives. Statuslinjen: «Analysen er oppdatert. Søknadsutkastet ditt er beholdt.» → [`mockups/key-resultater.html`](mockups/key-resultater.html) |
| **S4 Nytt søknadsutkast** | Seksjon 4 | Mens genereringen pågår, er alt låst som i S1. Deretter er teksten byttet og merket fjernet (FR-11). |
| **D Dialog** | Over siden | Se Bekreftelsesdialog i Component Patterns. → [`mockups/key-resultater.html`](mockups/key-resultater.html) |
| **E1 Feil fra AI-tjenesten** | Seksjon 1 eller 4 | Varselboks med melding etter type og «Prøv igjen». Teksten brukeren har limt inn og alle resultater er beholdt (FR-19). Et ufullstendig svar vises aldri som resultat. «Prøv igjen» sender teksten som står i feltene nå, etter ny lengdekontroll. → [`mockups/key-lasting-og-feil.html`](mockups/key-lasting-og-feil.html) |
| **E2 Ugyldig API-nøkkel** | Seksjon 1 (analyse) eller seksjon 4 (nytt søknadsutkast) | Varselboks med «Gå til demomodus» og «Lukk». Modus byttes aldri automatisk (FR-18). Velger brukeren demomodus, går siden til M0 med banner. Den innlimte teksten og alle resultater forsvinner. Varselteksten sier fra om dette. → [`mockups/key-lasting-og-feil.html`](mockups/key-lasting-og-feil.html) |
| **Ingen forslag** | Seksjon 3 | Tom-tekst i stedet for kort. Det er ikke en feil (FR-8). |
| **Tom kravgruppe** | Seksjon 2 | Tom-tekst under gruppetittelen. |
| **M0 Demomodus, ingen valgt** | Hele siden | Banner. Seksjon 1 med T1–T6 der ingen er valgt, tomme låste felt, «Vis analyse» deaktivert og «Analyser på nytt» deaktivert med forklaring. Ingen personvernboks (FR-22). |
| **M1 Demomodus, lagrede svar** | Hele siden | Som S2, med metadatalinje i seksjon 2, «Analyser på nytt» og «Generer nytt søknadsutkast» deaktivert med forklaring, og redigering og kopiering aktive (FR-15). Merket «Basert på forrige analyse» vises ikke. → [`mockups/key-demomodus.html`](mockups/key-demomodus.html) |
| **M2 Bytte testkombinasjon** | Demomodus | Når brukeren velger en annen T, fylles bare feltene i seksjon 1. Ved «Vis analyse» byttes seksjon 2–4. Er søknadsutkastet redigert, vises dialog D først. «Behold mitt utkast» setter valget og feltene tilbake til kombinasjonen som vises, og resultatene er uendret. |
| **Bekreftelse fjernet** | Seksjon 1 | «Analyser» / «Analyser på nytt» deaktiveres med hjelpeteksten. Resultatene blir stående. |
| **Omlasting / lukking** | Hele siden | Alt innhold og bekreftelsen er borte. Siden starter i S0 eller M0 (FR-20). Det er ikke designet noe varsel før brukeren forlater siden (tilleggsmål). |

## Interaction Primitives

- **Mus og tastatur likeverdig.** Alt kan gjøres med Tab, Shift+Tab, mellomrom og Enter. Det er ingen egne hurtigtaster, dra-og-slipp eller funksjoner som bare virker ved hover.
- **Enter i et tekstfelt gir linjeskift.** Analysen startes bare med knappen.
- **Én AI-handling om gangen.** Mens en analyse eller et nytt søknadsutkast pågår, er begge AI-knappene («Analyser»/«Analyser på nytt» og «Generer nytt søknadsutkast») låst, og CV-feltet, annonsefeltet og søknadsutkastet er skrivebeskyttet. Kopiering virker. Det finnes ingen kø (FR-1, FR-11). Dermed kan ingen omgå bekreftelsen i FR-11 ved å redigere under et kall.
- **Ingen automatiske handlinger.** Appen analyserer aldri mens brukeren skriver, bytter aldri modus selv, og overskriver aldri et redigert utkast uten å spørre.
- **Rulling og fokus:** etter første vellykkede analyse ruller siden til seksjon 2, og fokus flyttes til overskriften «2 Kravanalyse». Etter ny analyse blir rulleposisjon og fokus stående, og statuslinjen melder «Analysen er oppdatert. Søknadsutkastet ditt er beholdt.»

## Accessibility Floor

Dette er minimumskravet til oppførsel (NFR-20). Kontrast står i DESIGN.md. Designet er ikke kontrollert mot WCAG 2.1 AA, og det skal ikke påstås at det er det.

- Alle felt har synlige etiketter knyttet til feltet (`<label>`). Tegnteller og feilmelding kobles til feltet med `aria-describedby`, og feil markeres med `aria-invalid`.
- Status for annonsekrav formidles med tekst («Dekket», «Ikke oppgitt», «Mangler»). Ikon og farge er ekstra. Tabellene har ekte tabellmarkering med kolonneoverskrifter.
- Tab-rekkefølgen følger leserekkefølgen. Fokusindikatoren (`{components.focus-indicator}`) er alltid synlig.
- Statuslinjen («Analyserer …», «Analysen er ferdig.», «Analysen er oppdatert …») og «Kopiert ✓» meldes med `aria-live="polite"`. Varselbokser bruker `role="alert"`.
- Ved feltfeil går fokus til det første feltet med feil. Ved feil fra AI-tjenesten går fokus til varselboksen. Etter første analyse går fokus til overskriften «2 Kravanalyse» (`tabindex="-1"`).
- Dialogen holder fokus inne i seg, lukkes med Esc og sender fokus tilbake dit det var.
- Deaktiverte knapper har forklaringen som synlig tekst, så den kan leses av alle.
- Demobanneret er en `role="status"`-region og står først i dokumentet.
- Testkombinasjonslisten er en radiogruppe med piltaster mellom valgene. Fordi valget bare fyller feltene, er det trygt at valget følger fokus.

## Responsive & Platform

Designet er laget for datamaskin med vindusbredde fra cirka 1024 px. Under det kan de to feltene i seksjon 1 legges under hverandre, men mobiltilpasning er et tilleggsmål og er ikke designet eller testet (NFR-21, PRD §7.3). Appen skal fungere i oppdaterte versjoner av vanlige nettlesere.

## Inspiration & Anti-patterns

- **Hentet fra skjemaer i offentlige tjenester og nettbanker:** nummererte steg, tydelige feltfeil rett ved feltet og nøkterne farger.
- **Forkastet: match-score, prosent eller fremdriftsmåler.** Appen gir en etterprøvbar oversikt, ikke en dom (PRD §6).
- **Forkastet: chat-grensesnitt.** Appen stiller ingen oppfølgingsspørsmål (PRD §6).
- **Forkastet: faner eller flere sider for resultatene.** Alt ligger på én side, slik at brukeren ser sammenhengen mellom krav, forslag og utkast.
- **Forkastet: «uthev i CV-teksten»-kobling mellom kildehenvisning og felt.** Det er ikke en del av PRD-en og ble ikke tatt med.

## Key Flows

### UJ-1. Emma tilpasser CV og søknad til en juniorstilling innen økonomi

Emma (24) er nyutdannet økonom og har funnet en annonse for junior økonomikonsulent. Det er kveld, hun har CV-en i Word i ett vindu og appen i nettleseren i et annet. Appen kjører i vanlig modus.

1. Emma ser seksjon 1 (S0). Hun limer inn CV-teksten og annonseteksten, og tegntellerne viser 2 214 og 1 418 tegn.
2. «Analyser» er fortsatt grå. Hun leser personvernboksen, fjerner telefonnummeret fra CV-teksten og krysser av for «Jeg har lest informasjonen». Knappen blir blå.
3. Hun trykker «Analyser» (S1). Det står «Analyserer CV-teksten mot stillingsannonsen …» i noen sekunder.
4. Siden ruller til «2 Kravanalyse» (S2). Under «Skal-krav» ser hun at bachelorgraden er dekket, med sitatet fra CV-en. Førerkort står som ✕ Mangler, og regnskapserfaring som ? Ikke oppgitt.
5. Hun leser de to CV-forbedringsforslagene og begynner å redigere søknadsutkastet.
6. Statusforklaringen («har du kompetansen, kan du legge den til og analysere på nytt») minner henne på studentprosjektet med bokføring. Hun ruller opp, legger det inn i CV-teksten og trykker «Analyser på nytt».
7. **Høydepunkt:** regnskapskravet står nå som ✓ Dekket med hennes egen setning som kildehenvisning (S3). Søknadsutkastet hennes er urørt og merket «Basert på forrige analyse». Hun ser at det appen sier om henne, står i CV-en, og at ingenting er funnet på.
8. Hun velger «Generer nytt søknadsutkast». Dialogen spør om hun vil erstatte teksten hun har endret. Hun velger «Erstatt», leser det nye utkastet (S4), justerer en setning og trykker «Kopier søknadsutkast».
9. Hun lukker fanen. Ingenting er lagret.

**Grensetilfelle:** hvis Emma bare limer inn to linjer av CV-en, viser feltet «CV-teksten er for kort til å analysere …», og ingenting sendes (S0a).
**Feil:** svarer ikke AI-tjenesten innen ett minutt, ser hun en varselboks med «Prøv igjen». Teksten og det forrige utkastet hennes er beholdt (E1).

### UJ-2. Ingrid, sensor i IBE160, kjører og prøver appen uten API-nøkkel

Ingrid har klonet repoet og startet appen etter README, uten `.env`-fil. Hun har mange innleveringer og vil raskt se at appen virker.

1. Appen åpnes med det gule demobanneret øverst (M0). Det står at hun ser lagrede svar for fiktive eksempler.
2. Hun velger «T1 – God match». Den fiktive CV-teksten og annonseteksten vises i låste felt, med forklaringen om README.
3. Hun trykker «Vis analyse». Resultatene vises med en gang, i samme visning som i vanlig modus, med metadatalinjen «Lagret svar, ikke fasit. T1 · Kjøring 1 · Modell … · Dato …» (M1).
4. Hun redigerer en setning i søknadsutkastet og kopierer det. Begge deler virker. «Analyser på nytt» og «Generer nytt søknadsutkast» er grå, med forklaringen «Krever vanlig modus med API-nøkkel».
5. Hun velger T3, og feltene viser de nye fiktive tekstene. Hun trykker «Vis analyse». Fordi hun har redigert utkastet, spør dialogen først. Hun velger «Erstatt» og ser flere krav med ✕ Mangler (M2).
6. Hun prøver T5 (kort CV med mange ? Ikke oppgitt) og T6 (engelsk annonse, norsk resultat, kildehenvisninger fortsatt ordrett fra den norske CV-en).
7. **Høydepunkt:** Ingrid har sett hele kjerneflyten, alle tre statusene og språkscenarioet uten nøkkel, konto eller kostnad. Hun kan sammenligne svarene med fasiten i repoet.

**Grensetilfelle, ugyldig nøkkel:** finnes det en nøkkel som ikke virker, ser hun varselboksen «AI-tjenesten godtok ikke API-nøkkelen» (E2). Først når hun trykker «Gå til demomodus», vises banneret.

## Sporbarhet til PRD

| Krav | Dekket av |
|---|---|
| FR-1 Innliming og start | Inndatafelt, Analyser-knapp, S0/S1 |
| FR-2 For kort input | S0a, tekst «For kort» |
| FR-3 Maksimal lengde | Tegnteller, S0a, tekst «For lang» |
| FR-4 Kravtype | Kravtabeller gruppert i Skal-krav / Ønskede kvalifikasjoner |
| FR-5 Status | Statusmerke, statusforklaring |
| FR-6 Kildehenvisning | Kildekolonne, ubekreftet kildehenvisning |
| FR-7 Engelsk annonse | Plassholder for annonsetekst, T6 i demomodus, ordrett kildehenvisning |
| FR-8 CV-forbedringsforslag | Forslagskort, tilstanden «Ingen forslag» |
| FR-9 Søknadsutkast | Seksjon 4, Kopier |
| FR-10 Ny analyse beholder utkast | S3, merket «Basert på forrige analyse» |
| FR-11 Nytt søknadsutkast | Generer nytt søknadsutkast, Bekreftelsesdialog, S4, E1 i seksjon 4, Én AI-handling om gangen |
| FR-12 Oppstart i demomodus | M0 |
| FR-13 Merking av demomodus | Demobanner |
| FR-14 Valg av testkombinasjon | Liste over testkombinasjoner |
| FR-15 Lagrede svar | M1, metadatalinje, «Analyser på nytt» og «Generer nytt søknadsutkast» deaktivert med forklaring |
| FR-16 Ingen AI-kall i demo | «Vis analyse» uten lasting, ingen personvernboks |
| FR-17 Skrivebeskyttede felt | Låste felt med README-henvisning |
| FR-18 Ugyldig API-nøkkel | E2 (seksjon 1 og seksjon 4) |
| FR-19 Andre feil | E1, tabellen over feilmeldinger |
| FR-20 Ingen permanent lagring | Omlasting/lukking, personverntekst |
| FR-21 Ingen logging av innhold | Varselboksen viser aldri brukerens tekst (logging avgjøres i arkitekturen) |
| FR-22 Informasjon og bekreftelse | Personvernboks, Analyser-knapp |
| NFR-19 Språk | Voice and Tone |
| NFR-20 Tilgjengelighet | Accessibility Floor, kontrast i DESIGN.md |
| NFR-21 Plattform | Foundation, Responsive & Platform |
| NFR-22 Ventetid | S1, feilmelding ved tidsavbrudd |

## Merknader til arkitektur

- **Forslagstype:** forslagskortene viser *Fremhev / Omformuler / Flytt*. Det krever at hvert CV-forbedringsforslag har et felt for type i datastrukturen. Hvis arkitekturen ikke tar det med, vises kortet uten kicker.
- **«Redigert»-flagg:** appen må holde rede på om søknadsutkastet er endret siden det ble laget (FR-11 og bytte av testkombinasjon). Flagget gjelder bare for økten.
- **Metadata i demomodus:** de lagrede svarene må ha kjøringsnummer, modell, promptversjon og dato (FR-15).
- **Statuslinjen** og låsing under AI-kall krever bare tilstand i klienten, ingen lagring.
