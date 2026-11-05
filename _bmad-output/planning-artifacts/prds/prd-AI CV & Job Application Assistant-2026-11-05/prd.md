---
title: "AI CV & Job Application Assistant – PRD"
status: final
created: 2026-11-05
updated: 2026-11-05
---

# PRD: AI CV & Job Application Assistant

## 0. Document Purpose

Denne PRD-en beskriver hva MVP-en av AI CV & Job Application Assistant skal gjøre. Leserne er gruppen, faglærer og sensor i IBE160, og de neste stegene i BMAD-flyten: UX, arkitektur og epics og stories. Den bygger på den reviderte Product Brief (`brief.md`, commit `be54fba`) og faglærerens tilbakemelding, og gjentar dem ikke. Product Brief oppdateres ikke; PRD-en og beslutningsloggen dokumenterer hvordan kravene er videreutviklet fra briefen.

Begrepene i ordlisten (§3) brukes nøyaktig i hele dokumentet. Brukerreisene (UJ-1 og UJ-2) er hypotetiske. Funksjonskravene (FR-1–FR-22), de tverrgående kravene (NFR-1–NFR-23) og suksessmålene (SM-1–SM-10, SM-C1–SM-C5) har faste nummer, slik at stories, tester og evaluering kan vise til dem. Foreløpige verdier er merket «foreløpig». Uavklarte spørsmål er merket [ÅPENT SPØRSMÅL] og samlet i §9. Bekreftede antakelser står i §10. Beslutningene bak dokumentet er ført i `.memlog.md` i samme mappe. Teknologi, leverandør og modell velges i arkitekturfasen.

## 1. Vision

AI CV & Job Application Assistant hjelper nyutdannede med å tilpasse CV og søknad til en konkret stillingsannonse. Utgangspunktet er det brukeren faktisk har skrevet i CV-en. Brukeren limer inn CV-tekst og annonsetekst. Appen viser hvilke annonsekrav CV-en dekker, hvilke som ikke er oppgitt, og hvilke CV-en viser at mangler. Den gir begrunnede CV-forbedringsforslag og et søknadsutkast som brukeren kontrollerer, redigerer og kopierer.

Det som skiller appen fra en generell AI-chat, er sporbarhet. Hvert dekkede annonsekrav har en kildehenvisning til CV-teksten som applikasjonen selv kontrollerer, og appen dikter ikke opp kvalifikasjoner. Appen gir ingen samlet match-score, men en konkret og etterprøvbar oversikt over annonsekrav, status og kildehenvisninger. Brukeren skal kunne stole på at det appen sier om bakgrunnen hennes, står i CV-en, og selv vurdere resten.

Behovet er en hypotese. Det er ikke bekreftet gjennom brukerundersøkelser. Prosjektet dokumenterer derfor ikke tidsbesparelse, jobbintervjuer eller jobbresultater. Det evaluerer funksjonalitet og KI-kvalitet på et kontrollert, fiktivt testsett, og om appen kan kjøres og etterprøves av andre.

## 2. Target User

### 2.1 Jobs To Be Done

*Antatte behov hos målgruppen. Dette er hypoteser, ikke resultater av brukerundersøkelser.*

- **Funksjonelt:** Se raskt hvilke krav i en stillingsannonse CV-en min dekker, og hva som ikke kommer frem.
- **Funksjonelt:** Få et søknadsutkast for akkurat denne stillingen som jeg kan redigere, i stedet for å starte fra blankt ark.
- **Emosjonelt:** Være trygg på at det jeg sender inn, er sant, og at verktøyet ikke har pyntet på erfaringen min.
- **Kontekstuelt:** Jeg søker min første relevante jobb, er usikker på hva arbeidsgivere legger vekt på, og har en generell CV.

**Sekundær bruker:** Sensor og faglærer i IBE160 skal kunne kjøre appen, prøve kjerneflyten og etterprøve testing og evaluering uten nøkkel eller kostnad (UJ-2).

### 2.2 Non-Users (v1)

- **Erfarne arbeidstakere med lang karriere:** De kan bruke appen, men flyten og testsettet er ikke laget for dem.
- **Arbeidsgivere og rekrutterere:** Appen vurderer ikke kandidater og rangerer ikke søkere.
- **De som trenger søknad eller grensesnitt på engelsk:** Stillingsannonsen kan være på engelsk, men resultatet er på norsk.
- **De som vil ha ferdig formatert CV eller lagre arbeid mellom økter.**

### 2.3 Key User Journeys

*Brukerreisene er hypotetiske og laget for å beskrive den tiltenkte flyten. De bygger ikke på dokumentert brukerforskning.*

- **UJ-1. Emma tilpasser CV og søknad til en juniorstilling innen økonomi.**
  - **Persona og kontekst:** Emma (24) er nyutdannet med bachelorgrad i økonomi og administrasjon og søker sin første relevante jobb. Hun har en generell CV, men er usikker på hva hun bør fremheve for akkurat denne stillingen.
  - **Utgangspunkt:** Hun har CV-en i Word og har funnet en stillingsannonse på FINN. Hun åpner webappen i nettleseren uten å logge inn, og appen har API-nøkkel (vanlig modus).
  - **Flyt:**
    1. Emma kopierer CV-teksten og annonseteksten inn i hvert sitt felt og starter analysen.
    2. Appen viser kravanalysen: hvert annonsekrav er merket som skal-krav eller ønsket kvalifikasjon og har status dekket, ikke oppgitt eller mangler. Dekkede annonsekrav viser kildehenvisningen, altså teksten fra CV-en som dekker annonsekravet.
    3. Under kravanalysen får hun relevante og begrunnede CV-forbedringsforslag, hvert knyttet til et annonsekrav, og et søknadsutkast som hun begynner å redigere.
    4. Et annonsekrav står som ikke oppgitt. Emma innser at et relevant studieprosjekt mangler i CV-en, legger det inn i CV-teksten og kjører analysen på nytt.
    5. Kravanalysen og CV-forbedringsforslagene oppdateres. Søknadsutkastet hennes beholdes og merkes «Basert på forrige analyse». Hun velger selv når et nytt søknadsutkast skal genereres.
  - **Høydepunkt:** Emma ser hvilke av kvalifikasjonene hennes som faktisk er dokumentert i CV-en, og hva hun kan forbedre, uten at appen har funnet på erfaring hun ikke har.
  - **Avslutning:** Hun kontrollerer søknadsteksten, kopierer den og tar den med videre til søknaden. Ingenting lagres i appen når hun lukker økten.
  - **Grensetilfelle:** Hvis Emma bare limer inn noen få linjer av CV-en, viser appen en forståelig melding om at teksten er for kort til å analysere, i stedet for et resultat. Den nøyaktige grensen fastsettes i funksjonskravene.

  **Funksjoner reisen krever** (FR-numrene settes i seksjon 4):
  - Systemet må ta imot innlimt CV-tekst og annonsetekst og starte en analyse. (steg 1)
  - Systemet må hente ut annonsekrav med kravtype og status, og vise kildehenvisning for dekkede annonsekrav. (steg 2)
  - Systemet må gi CV-forbedringsforslag knyttet til annonsekrav, og bare der det finnes et reelt forbedringsbehov. (steg 3)
  - Systemet må lage et redigerbart og kopierbart søknadsutkast. (steg 3 og avslutning)
  - Systemet må kunne kjøre en ny analyse som oppdaterer kravanalysen og CV-forbedringsforslagene, men beholder det eksisterende søknadsutkastet (redigert eller ikke), merker det «Basert på forrige analyse» og lar brukeren selv velge når et nytt søknadsutkast skal genereres. Dette skal bli et testbart krav. (steg 4–5)
  - Systemet må avvise for kort input med en forståelig melding. Dette skal knyttes til et testbart akseptansekriterium. (grensetilfelle)

- **UJ-2. Ingrid, sensor i IBE160, kjører og prøver appen uten API-nøkkel.**
  - **Persona og kontekst:** Ingrid er sensor i IBE160 og vurderer del 1 av mappen. Hun skal kontrollere at appen gjør det briefen og PRD-en beskriver, at den er testet, og at den kan kjøres etter README. Hun har ingen API-nøkkel, ingen konto hos AI-tjenesten og ingen tilgang til gruppens tjenester. Hun bruker tid på flere innleveringer og vil raskt se om appen virker.
  - **Utgangspunkt:** Hun har klonet repoet fra GitHub til sin egen maskin. Kjøretidsmiljøet README-en oppgir (velges i arkitekturfasen), er installert eller kan installeres gratis (bekreftet antakelse, §10). Hun oppretter ingen `.env`-fil.
  - **Flyt:**
    1. Ingrid følger README: hun installerer avhengigheter og starter appen med kommandoene som står der, uten å oppgi noen API-nøkkel.
    2. Appen starter i demomodus. Et tydelig merke forteller at hun ser lagrede svar for fiktive eksempler, og at analyse av egen tekst krever API-nøkkel.
    3. Hun velger testkombinasjon T1 (god match) fra en liste. Den fiktive CV-teksten og annonseteksten vises, og hun starter analysen.
    4. Appen viser de lagrede svarene i samme visning som i vanlig modus: kravanalyse med kravtype, status og kildehenvisning, CV-forbedringsforslag og et søknadsutkast hun kan redigere og kopiere. Visningen oppgir kjøringsnummer, modell, promptversjon og dato for de lagrede svarene.
    5. Hun prøver T3 (svak match) og T5 (kort CV med lite informasjon) for å se hvordan appen viser annonsekrav med status mangler og ikke oppgitt. Til slutt prøver hun T6, der stillingsannonsen er på engelsk og resultatet på norsk.
    6. Hun kjører de automatiske testene med kommandoen i README. De bruker kontrollerte mock-data og består uten API-nøkkel og uten nettverkstilgang til AI-tjenesten. README sier tydelig at testene viser at funksjonaliteten virker, ikke at KI-analysen er korrekt.
  - **Høydepunkt:** Ingrid får sett hele kjerneflyten uten nøkkel, konto eller kostnad. Hun kan sammenligne de lagrede KI-svarene med den separate, kontrollerte fasiten i repoet.
  - **Avslutning:** Hun har kjørt appen og testene etter README og kan vurdere funksjonalitet, design og testing. Kvaliteten på KI-analysen vurderer hun ut fra resultattabellen fra evalueringen, der grunnsettet T1–T5 og språkscenarioet T6 er rapportert hver for seg.
  - **Grensetilfeller:**
    - **Egen tekst i demomodus:** Hvis Ingrid prøver å lime inn egen tekst, analyserer appen den ikke. Den forklarer at demomodus bare støtter de forhåndsdefinerte testkombinasjonene, og viser hvor README forklarer vanlig modus.
    - **Ugyldig nøkkel:** Hvis det finnes en API-nøkkel som ikke virker, krasjer ikke appen. Den viser en forståelig feilmelding og tilbyr brukeren å gå til demomodus. Appen bytter ikke automatisk uten å informere brukeren, og demomodus er tydelig merket også når den er valgt på denne måten.
    - **Uten nett:** Demomodus gjør ingen kall til AI-tjenesten, så den virker også uten nettverkstilgang etter at avhengighetene er installert.

  **Funksjoner reisen krever** (FR-numrene settes i seksjon 4):
  - Systemet må starte i demomodus når API-nøkkel mangler, uten feil og uten ekstra oppsett. (steg 1–2)
  - Systemet må merke demomodus tydelig i grensesnittet så lenge den er aktiv, uansett hvordan den ble startet. (steg 2, grensetilfelle)
  - Systemet må la brukeren velge blant de forhåndsdefinerte testkombinasjonene og vise den fiktive CV-teksten og annonseteksten. (steg 3)
  - Systemet må vise lagrede svar i samme visning og med samme funksjoner som i vanlig modus, også redigering og kopiering av søknadsutkastet, og oppgi modell og dato for svarene. (steg 4–5)
  - Systemet må ikke gjøre kall til den eksterne AI-tjenesten i demomodus. (grensetilfelle)
  - Systemet må avvise analyse av egen tekst i demomodus med en forståelig forklaring. (grensetilfelle)
  - Systemet må håndtere en ugyldig API-nøkkel med en forståelig feilmelding og tilby overgang til demomodus etter brukerens valg. (grensetilfelle)
  - Repoet må inneholde README med oppstart og testkjøring, `.env.example`, de fiktive testdataene, en separat kontrollert fasit, lagrede KI-svar for hver testkombinasjon med modell og dato, og resultattabellen fra evalueringen. (steg 1, 6 og avslutning)
  - De automatiske testene må kunne kjøres uten API-nøkkel, med kontrollerte mock-data. De skal blant annet verifisere at et eksisterende søknadsutkast, redigert eller ikke, beholdes ved ny analyse, merkes «Basert på forrige analyse», og at brukeren kan velge å generere nytt søknadsutkast. (steg 6)

## 3. Glossary

*Alle seksjoner bruker disse begrepene nøyaktig. I forklarende tekst brukes «stillingsannonse» om selve annonsen; «annonsetekst» er navnet på inputfeltet og teksten som limes inn i det. Ordlisten forutsetter ingen teknologivalg utover det briefen har bestemt; resten avgjøres i arkitekturfasen.*

**Input og analyse**
- **CV-tekst** — Teksten brukeren limer inn fra sin CV. Én per analyse.
- **Annonsetekst** — Inputfeltet for stillingsannonsen og teksten som limes inn i det. Stillingsannonsen kan være på norsk eller engelsk. Én per analyse.
- **For kort input** — CV-tekst eller annonsetekst under minimumslengden som fastsettes i FR. Gir en forståelig melding i stedet for en analyse.
- **Analyse** — Én kjøring som ut fra én CV-tekst og én annonsetekst gir en kravanalyse og CV-forbedringsforslag, og et søknadsutkast dersom økten ikke allerede har et.
- **Ny analyse** — En analyse brukeren kjører etter å ha endret CV-teksten eller annonseteksten i samme økt. Erstatter kravanalysen og CV-forbedringsforslagene. Et eksisterende søknadsutkast beholdes, redigert eller ikke.
- **Økt** — Perioden appen er åpen i nettleseren. Applikasjonen lagrer ikke CV-tekst, annonsetekst eller analyseresultater permanent; alt forsvinner når økten avsluttes. Eventuell behandling eller lagring hos AI-tjenesten er et eget forhold som omtales i personvernkravene.

**Resultater**
- **Annonsekrav** — Ett krav eller én kvalifikasjon hentet ut av stillingsannonsen. Hvert annonsekrav har nøyaktig én kravtype og én status.
- **Kravtype** — Enten *skal-krav* (stillingsannonsen stiller det som krav) eller *ønsket kvalifikasjon* (stillingsannonsen ønsker det, men krever det ikke).
- **Status** — Én av tre verdier per annonsekrav:
  - *dekket*: CV-teksten inneholder opplysninger som oppfyller annonsekravet.
  - *ikke oppgitt*: CV-teksten sier ingenting som avgjør om annonsekravet er oppfylt. Fravær av opplysninger gir alltid *ikke oppgitt*.
  - *mangler*: CV-teksten dokumenterer eksplisitt at annonsekravet ikke er oppfylt, for eksempel bachelorgrad der stillingsannonsen krever master. Brukes aldri bare fordi opplysninger mangler.
- **Kildehenvisning** — Et ordrett utdrag av CV-teksten som begrunner statusen *dekket*. Påkrevd for hvert dekket annonsekrav.
- **Kravanalyse** — Listen over alle annonsekrav i én analyse, med kravtype, status og eventuell kildehenvisning.
- **CV-forbedringsforslag** — Et begrunnet forslag om å fremheve, omformulere eller flytte innhold som allerede står i CV-teksten. Knyttet til minst ett annonsekrav. Gis bare der det finnes et reelt forbedringsbehov.
- **Søknadsutkast** — Et utkast til søknadstekst på norsk for stillingen i stillingsannonsen. Kan redigeres og kopieres. Beholdes ved ny analyse, redigert eller ikke, og merkes da «Basert på forrige analyse» til brukeren selv genererer et nytt søknadsutkast.
- **Oppdiktet kvalifikasjon** — Utdanning, erfaring eller ferdighet i et CV-forbedringsforslag eller søknadsutkast som ikke står i CV-teksten. Aldri tillatt.

**Moduser**
- **Vanlig modus** — Appen kjører med gyldig API-nøkkel og analyserer CV-tekst og annonsetekst brukeren limer inn, ved hjelp av AI-tjenesten.
- **Demomodus** — Appen viser lagrede svar for de forhåndsdefinerte testkombinasjonene T1–T6, uten API-nøkkel og uten kall til AI-tjenesten. Alltid tydelig merket. Analyserer ikke egen tekst.
- **AI-tjeneste** — Den eksterne språkmodelltjenesten som brukes i vanlig modus. Tilbys av en *AI-leverandør*. Leverandør og modell velges i arkitekturfasen.
- **API-nøkkel** — Nøkkelen til AI-tjenesten. Oppgis i lokal konfigurasjon som ikke committes; repoet har en eksempelfil uten nøkkel.

**Testing og evaluering**
- **Testkombinasjon** — Én fiktiv CV og én fiktiv stillingsannonse med tilhørende fasit. Grunnsettet er T1–T5 (CV1–CV5 med A1–A5). T6 er språkscenarioet: CV1 med den engelske stillingsannonsen A6 og norsk resultat. T6 rapporteres separat.
- **Fasit** — Det gruppen på forhånd og manuelt har kontrollert for en testkombinasjon: annonsekravene, forventet kravtype og status, og hvor det finnes et reelt forbedringsbehov. Hentes aldri fra KI-svar.
- **Lagret svar** — Det første gyldige og fullstendige KI-svaret fra evalueringen av én testkombinasjon, lagret med kjøringsnummer, modell, promptversjon og dato. Gyldig og fullstendig betyr at svaret kan tolkes fullstendig og oppfyller forventet datastruktur (jf. FR-19). Svaret velges ikke ut i etterkant fordi det gir et bedre inntrykk. Brukes i demomodus. Er ikke fasit.
- **Mock-data** — Kontrollerte, konstruerte svar som brukes i automatiske tester for å teste funksjonaliteten uten AI-tjenesten. Dokumenterer ikke at KI-analysen er korrekt.
- **Evaluering** — Manuell kontroll av KI-svar for hver testkombinasjon mot fasiten og sjekklisten, i vanlig modus med en gitt modell.
- **Resultattabell** — Dokumentasjon av evalueringen i repoet, med modell, promptversjon og dato. Grunnsettet T1–T5 og språkscenarioet T6 rapporteres hver for seg.

## 4. Features

### 4.1 Innliming og start av analyse

**Description:** Brukeren limer inn CV-tekst og annonsetekst i hvert sitt felt og starter en analyse. Realiserer UJ-1 steg 1 og grensetilfellet med for kort input.

#### FR-1: Innliming av CV-tekst og annonsetekst

Brukeren kan lime inn CV-tekst og annonsetekst i to separate felt og starte en analyse i vanlig modus. Realiserer UJ-1.

**Consequences (testable):**
- Analysen kan bare startes når begge feltene har tekst.
- Mens analysen pågår, vises en lasteindikator, og analysen kan ikke startes på nytt samtidig.
- Innlimt tekst blir stående i feltene etter analysen, slik at brukeren kan endre den og kjøre ny analyse.

#### FR-2: For kort input

Systemet avviser for kort input med en forståelig melding i stedet for å analysere. Realiserer UJ-1 (grensetilfelle).

**Consequences (testable):**
- CV-tekst under 300 tegn eller annonsetekst under 200 tegn, regnet uten mellomrom i start og slutt, er for kort input. Grensene er foreløpige.
- Ved for kort input sendes ingenting til AI-tjenesten, og meldingen sier hvilket felt som er for kort.
- Tomt felt behandles som for kort input.
- Automatiske tester verifiserer oppførselen rett under og rett over hver grense.
- Ingen av de fiktive CV-ene eller stillingsannonsene i testsettet, heller ikke den korte CV5, avvises av grensene. Dette kontrolleres når testdataene er laget.

#### FR-3: Maksimal lengde

Systemet begrenser lengden på CV-tekst og annonsetekst for å holde kostnaden per analyse lav.

**Consequences (testable):**
- Maksimalt 15 000 tegn per felt. Grensen er foreløpig.
- Tekst over grensen avvises med en melding om hvor mye som må kortes ned. Teksten kuttes ikke uten at brukeren vet det.
- Automatiske tester verifiserer oppførselen rett under og rett over grensen.

**Notes:** Grensen vurderes i arkitektur- og implementeringsfasen opp mot valgt modell, API-kostnad og de reelle testdataene.

### 4.2 Kravanalyse

**Description:** Systemet henter ut annonsekravene fra stillingsannonsen, gir hvert annonsekrav kravtype og status, og begrunner statusen *dekket* med kildehenvisning. Realiserer UJ-1 steg 2.

#### FR-4: Uttrekk av annonsekrav med kravtype

Systemet henter ut annonsekravene fra annonseteksten og gir hvert annonsekrav nøyaktig én kravtype: skal-krav eller ønsket kvalifikasjon. Realiserer UJ-1.

**Consequences (testable):**
- Hvert annonsekrav har nøyaktig én kravtype.
- Skal-krav og ønskede kvalifikasjoner vises tydelig adskilt eller merket, slik at brukeren ser hvilke som er skal-krav.
- **Uttrekk måles for seg:** I evalueringen sammenlignes kravanalysen manuelt med fasiten. Et annonsekrav i fasiten regnes som *funnet* når kravanalysen har et annonsekrav med samme innhold. Kravet er at alle annonsekrav i fasiten blir funnet (sjekkliste punkt 1). Annonsekrav i kravanalysen som ikke finnes i fasiten, telles og rapporteres i resultattabellen.
- **Kravtype måles for seg:** Andelen funne annonsekrav med riktig kravtype rapporteres i resultattabellen. [ÅPENT SPØRSMÅL] Product Brief fastsetter ingen terskel for kravtype, fordi kravtype ble innført i PRD-arbeidet. Terskelen avklares før evalueringen kjøres (§9, spørsmål 1).

#### FR-5: Klassifisering av status

Systemet gir hvert annonsekrav nøyaktig én status: dekket, ikke oppgitt eller mangler.

**Consequences (testable):**
- *Mangler* brukes bare når CV-teksten eksplisitt dokumenterer at annonsekravet ikke er oppfylt. Fravær av opplysninger gir *ikke oppgitt*. Fasiten for testsettet inneholder annonsekrav av begge slag, og evalueringen kontrollerer dette skillet.
- **Status måles for seg:** I evalueringen stemmer statusen med fasiten for minst 80 % av de funne annonsekravene i hver testkombinasjon (sjekkliste punkt 3). Andelen beregnes bare over annonsekrav som er funnet, og dokumenterer ikke at alle annonsekrav er funnet. Det måles i FR-4.

#### FR-6: Kildehenvisning for dekkede annonsekrav

Hvert annonsekrav med status *dekket* viser en kildehenvisning: et ordrett utdrag av CV-teksten.

**Consequences (testable):**
- Systemet kontrollerer automatisk at kildehenvisningen finnes ordrett i CV-teksten. Forskjeller i mellomrom og linjeskift godtas. Alle andre tekstlige forskjeller, også store/små bokstaver, tegnsetting, omskriving og oversettelse, gir ikke ordrett treff.
- Kildehenvisningen vises slik den står i CV-teksten, uten omskriving eller oversettelse.
- Et annonsekrav der kildehenvisningen ikke kan bekreftes, presenteres aldri som dekket. Det får status *ikke oppgitt* og en tydelig advarsel om at kildehenvisningen ikke kunne bekreftes. Den ugyldige henvisningen vises ikke som dokumentasjon.
- I evalueringen skilles det mellom rått KI-svar og resultatet etter applikasjonens validering. En ugyldig kildehenvisning i det rå KI-svaret teller som feil i evalueringen av KI-kvalitet (sjekkliste punkt 2), også når applikasjonen oppdager den. Antallet ugyldige kildehenvisninger som applikasjonen fanget opp, rapporteres i resultattabellen.
- Automatiske tester med mock-data verifiserer at en kildehenvisning som ikke finnes i CV-teksten, blir oppdaget, og at en kildehenvisning som bare skiller seg i mellomrom og linjeskift, godtas.

#### FR-7: Stillingsannonse på engelsk

Systemet analyserer en stillingsannonse på engelsk og leverer kravanalyse, CV-forbedringsforslag og søknadsutkast på norsk.

**Consequences (testable):**
- T6 (CV1 + A6) evalueres med samme sjekkliste som grunnsettet og rapporteres separat.
- Kildehenvisninger er fortsatt ordrette utdrag av CV-teksten. De oversettes ikke.

### 4.3 CV-forbedringsforslag

**Description:** Systemet gir begrunnede CV-forbedringsforslag om hvordan innhold som allerede står i CV-teksten kan fremheves, omformuleres eller flyttes. Realiserer UJ-1 steg 3.

#### FR-8: CV-forbedringsforslag

Systemet gir CV-forbedringsforslag der det finnes et reelt forbedringsbehov.

**Consequences (testable):**
- Hvert CV-forbedringsforslag er knyttet til minst ett annonsekrav og har en kort begrunnelse.
- Ingen CV-forbedringsforslag inneholder en oppdiktet kvalifikasjon (sjekkliste punkt 4).
- Der fasiten viser et reelt forbedringsbehov, gir systemet et relevant CV-forbedringsforslag (sjekkliste punkt 5). Der fasiten ikke viser noe behov, er det ikke en feil at det ikke gis CV-forbedringsforslag.

### 4.4 Søknadsutkast og ny analyse

**Description:** Systemet lager et søknadsutkast på norsk som brukeren kan redigere og kopiere. Ved ny analyse beholdes søknadsutkastet, og brukeren bestemmer selv når et nytt skal genereres. Realiserer UJ-1 steg 3–5 og avslutningen.

#### FR-9: Søknadsutkast

Systemet lager et søknadsutkast på norsk ved første analyse i økten.

**Consequences (testable):**
- Søknadsutkastet gjelder stillingen i stillingsannonsen og inneholder ingen oppdiktet kvalifikasjon (sjekkliste punkt 4 og 6).
- Brukeren kan redigere søknadsutkastet direkte og kopiere hele teksten med én handling.

#### FR-10: Ny analyse beholder søknadsutkastet

Brukeren kan kjøre ny analyse etter å ha endret CV-teksten eller annonseteksten. Realiserer UJ-1 steg 4–5.

**Consequences (testable):**
- Kravanalysen og CV-forbedringsforslagene erstattes med resultatene fra den nye analysen.
- Et eksisterende søknadsutkast, redigert eller ikke, beholdes uendret og merkes «Basert på forrige analyse».
- Automatiske tester med mock-data verifiserer begge punktene.

#### FR-11: Generere nytt søknadsutkast

Brukeren kan selv velge å generere et nytt søknadsutkast basert på siste analyse.

**Consequences (testable):**
- Har brukeren redigert søknadsutkastet manuelt, ber systemet om bekreftelse før det blir erstattet. Avbryter brukeren, beholdes søknadsutkastet uendret.
- Mens genereringen pågår, vises en lasteindikator, og ny generering kan ikke startes samtidig.
- Lykkes genereringen, erstatter det nye søknadsutkastet det gamle, og merket «Basert på forrige analyse» fjernes.
- Feiler genereringen, beholdes det eksisterende søknadsutkastet uendret, med eventuelt merke, og brukeren får en forståelig feilmelding.
- Automatiske tester med mock-data verifiserer bekreftelse, vellykket generering, at merket forsvinner, og at søknadsutkastet beholdes ved feil.

**Notes:** I vanlig modus gir generering av nytt søknadsutkast et ekstra kall til AI-tjenesten og dermed en ekstra kostnad.

### 4.5 Demomodus

**Description:** Uten API-nøkkel viser appen lagrede svar for de forhåndsdefinerte testkombinasjonene T1–T6, slik at sensor og andre kan prøve hele flyten uten nøkkel, konto eller kostnad. Realiserer UJ-2.

#### FR-12: Oppstart i demomodus

Systemet starter i demomodus når API-nøkkel mangler. Realiserer UJ-2 steg 1–2.

**Consequences (testable):**
- Uten API-nøkkel starter appen uten feil og uten annet oppsett enn det README beskriver.
- Automatiske tester verifiserer at appen velger demomodus når API-nøkkel mangler.

#### FR-13: Merking av demomodus

Systemet merker demomodus tydelig så lenge den er aktiv. Realiserer UJ-2 steg 2.

**Consequences (testable):**
- Merket er synlig på alle skjermbilder i demomodus, også når demomodus er valgt etter feil med API-nøkkelen (FR-18).
- Merket forteller at resultatene er lagrede svar for fiktive eksempler, og at analyse av egen tekst krever vanlig modus og API-nøkkel.

#### FR-14: Valg av testkombinasjon

Brukeren kan velge en av testkombinasjonene T1–T6 i demomodus. Realiserer UJ-2 steg 3 og 5.

**Consequences (testable):**
- Listen viser T1–T6 med en kort beskrivelse av situasjonen. T6 er merket som språkscenario (engelsk stillingsannonse, norsk resultat).
- Når en testkombinasjon er valgt, vises den fiktive CV-teksten og annonseteksten.

#### FR-15: Visning av lagrede svar

Systemet viser lagrede svar i samme visning og med samme funksjoner som i vanlig modus, med unntakene under. Realiserer UJ-2 steg 4–5.

**Consequences (testable):**
- Kravanalyse, CV-forbedringsforslag og søknadsutkast vises på samme måte som i vanlig modus. Kontrollen av kildehenvisninger (FR-6) gjelder også lagrede svar.
- Det eksisterende søknadsutkastet kan redigeres og kopieres.
- Visningen oppgir kjøringsnummer, modell, promptversjon og dato for det lagrede svaret og kaller det ikke fasit.
- Ny analyse og generering av nytt søknadsutkast er deaktivert, med en tydelig forklaring om at funksjonene krever vanlig modus og API-nøkkel.
- Automatiske tester verifiserer at hver av T1–T6 har et lagret svar som kan vises, og at ny analyse og nytt søknadsutkast er deaktivert.

#### FR-16: Ingen kall til AI-tjenesten i demomodus

Systemet gjør ingen kall til AI-tjenesten i demomodus. Realiserer UJ-2 (grensetilfelle).

**Consequences (testable):**
- Automatiske tester verifiserer at det ikke gjøres noe kall til AI-tjenesten i demomodus.
- Demomodus virker uten nettverkstilgang etter at avhengighetene er installert.

#### FR-17: Skrivebeskyttede felt i demomodus

Feltene for CV-tekst og annonsetekst er skrivebeskyttet i demomodus. Realiserer UJ-2 (grensetilfelle).

**Consequences (testable):**
- Brukeren kan ikke endre teksten i feltene i demomodus.
- Grensesnittet forklarer at demomodus bare støtter de forhåndsdefinerte testkombinasjonene, og viser hvor README forklarer vanlig modus.

### 4.6 Feilhåndtering mot AI-tjenesten

**Description:** Feil mot AI-tjenesten skal aldri krasje appen eller slette det brukeren har lagt inn. Realiserer UJ-2 (grensetilfelle) og beskytter UJ-1.

#### FR-18: Ugyldig API-nøkkel

Systemet håndterer en API-nøkkel som avvises av AI-tjenesten. Realiserer UJ-2.

**Consequences (testable):**
- Appen viser en forståelig feilmelding og tilbyr brukeren å gå til demomodus.
- Appen går ikke over i demomodus før brukeren har valgt det. Når brukeren velger det, er demomodus merket som i FR-13.
- Automatiske tester med mock-data verifiserer melding, tilbud og at det ikke byttes modus automatisk.

#### FR-19: Andre feil fra AI-tjenesten

Systemet håndterer tidsavbrudd, nettverksfeil, kvote- eller kostnadsgrenser og KI-svar som ikke kan tolkes.

**Consequences (testable):**
- Brukeren får en forståelig feilmelding og kan prøve igjen.
- CV-teksten, annonseteksten og eventuelle tidligere resultater, også søknadsutkastet, beholdes uendret.
- Et KI-svar som ikke kan tolkes fullstendig, eller som ikke oppfyller forventet datastruktur, behandles som feil. Ufullstendige resultater vises ikke som en fullført analyse.
- Automatiske tester med mock-data verifiserer hver feiltype, også et ufullstendig KI-svar.

### 4.7 Personvern i applikasjonen

**Description:** Applikasjonen lagrer ikke CV-tekst, annonsetekst eller resultater permanent, og brukeren får vite at tekst sendes til AI-tjenesten. Hvordan AI-leverandøren behandler data, omtales i personvernkravene, ikke her.

#### FR-20: Ingen permanent lagring

Applikasjonen lagrer ikke CV-tekst, annonsetekst eller analyseresultater permanent.

**Consequences (testable):**
- Ingenting av dette lagres i database, i filer eller i nettleserens lagring.
- Når siden lastes på nytt eller lukkes, er innholdet borte.

**Notes:** Varsel før brukeren forlater siden med innhold er et tilleggsmål, ikke et MVP-krav, fordi nettlesere kan begrense slike varsler.

#### FR-21: Ingen logging av innhold

Applikasjonen skriver ikke CV-tekst, annonsetekst eller analyseresultater til egne logger.

**Consequences (testable):**
- Feilmeldinger og logger inneholder feiltype, men ikke innholdet brukeren har lagt inn.
- Automatiske tester verifiserer at en feil under analyse ikke skriver innholdet til loggen.

#### FR-22: Informasjon og bekreftelse før tekst sendes til AI-tjenesten

Brukeren får tydelig informasjon om at CV-teksten og annonseteksten sendes til en ekstern AI-tjeneste, og må aktivt bekrefte at informasjonen er lest før første analyse i vanlig modus.

**Consequences (testable):**
- Analysen kan ikke startes i vanlig modus før brukeren har bekreftet informasjonen.
- Informasjonen oppfordrer brukeren til å fjerne unødvendige personopplysninger, som telefonnummer, e-postadresse og adresse, før innliming.
- Bekreftelsen omtales som bekreftelse på at informasjonen er lest, ikke som juridisk samtykke etter GDPR.
- Informasjonen og bekreftelsen vises ikke i demomodus, der ingenting sendes.
- Bekreftelsen gjelder for resten av økten, men lagres ikke permanent (jf. FR-20).
- Automatiske tester verifiserer at analysen ikke kan startes før bekreftelsen er gitt.

## 5. Tverrgående krav og rammer

*Kravene gjelder hele applikasjonen. De beskriver hva som må oppfylles, ikke hvordan. Teknologi, leverandør og modell velges i arkitekturfasen.*

### 5.1 Personvern hos AI-leverandøren

- **NFR-1 Fiktive data:** Utvikling, automatiske tester, evaluering og demomodus bruker bare fiktive data. Ingen ekte CV-er, heller ikke gruppemedlemmenes egne, legges i repoet.
- **NFR-2 Dokumentasjon av leverandør:** Når AI-tjenesten er valgt, dokumenteres følgende i arkitekturen og kortfattet i README, med henvisning til leverandørens egne vilkår:
  - hvilke data som sendes
  - om API-data brukes til modelltrening
  - hvor lenge data lagres hos leverandøren
  - hvor data behandles

  Står noe av dette ikke i vilkårene, skrives det at det er uavklart. Det skal ikke antas.
- **NFR-3 Utvalgskriterium:** En leverandør som dokumenterer at API-data ikke brukes til modelltrening, foretrekkes, så langt det er forenlig med budsjettet (NFR-8).
- **NFR-4 Ingen juridiske påstander:** PRD, grensesnitt og README påstår ikke at løsningen er GDPR-kompatibel. Personvernvalgene beskrives som det de er: valg gjort i et studentprosjekt med fiktive testdata.

### 5.2 API-kostnad

- **NFR-5 Utvalgskriterium:** AI-tjenesten velges med mål om lavest mulig kostnad, helst en rimelig modell eller et gratisnivå.
- **NFR-6 Kall bare der det trengs:** Under utvikling og i automatiske tester brukes mock-data. Reelle kall skjer bare ved manuell prøving i vanlig modus og ved evaluering. Demomodus gjør ingen kall (FR-16).
- **NFR-7 Begrensede kall:** Lengden på input er begrenset (FR-3). Hver analyse og hver generering av nytt søknadsutkast gir et avgrenset antall kall, som fastsettes i arkitekturen.
- **NFR-8 Budsjett og kostnadsoverslag:** Foreløpig budsjettramme er 200 kr for samlede API-kostnader i prosjektet. Rammen er et forslag som må bekreftes av gruppen. Når modell er valgt, dokumenteres et overslag over kostnad per analyse og for en full evaluering (NFR-13).

### 5.3 Testing og kvalitetssikring

- **NFR-9 To nivåer som rapporteres hver for seg:**
  1. **Automatiske tester med mock-data** verifiserer funksjonaliteten (FR-1–FR-22) og kan kjøres uten API-nøkkel og uten nettverk.
  2. **Evaluering av KI-kvalitet** kontrollerer rå KI-svar for hver testkombinasjon mot fasiten og sjekklisten.

  Beståtte automatiske tester presenteres aldri som dokumentasjon på at KI-analysen er korrekt.
- **NFR-10 Fasit først:** Fasiten for hver testkombinasjon lages og kontrolleres manuelt før evalueringen kjøres. Den hentes aldri fra KI-svar.
- **NFR-11 Resultattabell:** Resultattabellen oppgir modell, promptversjon og dato og rapporterer per testkombinasjon og per kjøring:
  - om alle annonsekrav er funnet, og antall ekstra annonsekrav
  - andel riktig kravtype
  - andel riktig status
  - antall ugyldige kildehenvisninger i rått KI-svar, og hvor mange applikasjonen fanget opp
  - antall oppdiktede kvalifikasjoner
  - bestått eller ikke bestått

  T1–T5 og T6 rapporteres hver for seg.
- **NFR-12 Ny evaluering ved endring:** Evalueringen gjelder én kombinasjon av promptversjon og modell. Ved vesentlige endringer i prompt eller modell gjennomføres evalueringen på nytt, og de lagrede svarene i demomodus oppdateres slik at de samsvarer med den dokumenterte modellen og promptversjonen.
- **NFR-13 Gjentatte kjøringer:** Hver testkombinasjon T1–T6 kjøres tre ganger uavhengig av hverandre, totalt 18 kjøringer, dersom budsjettet tillater det. Resultatene rapporteres per kjøring, og variasjonen mellom kjøringene oppsummeres. Gjør kostnad eller tid dette urealistisk, kan antallet reduseres til én kjøring per testkombinasjon, men begrensningen dokumenteres. Tre kjøringer viser om resultatene varierer i dette testsettet. De er ikke statistisk sikker dokumentasjon på modellens generelle kvalitet. Regler for bestått står i §8; feil skjules ikke gjennom gjennomsnitt.

### 5.4 Kjørbarhet for sensor

- **NFR-14 Uten nøkkel og konto:** Appen kan klones, installeres og startes etter README uten API-nøkkel, betalte kontoer eller tilgang til gruppens tjenester. Den starter da i demomodus.
- **NFR-15 README:** README beskriver:
  - forutsetninger
  - installasjon og oppstart
  - kjøring av automatiske tester
  - hva demomodus er
  - hvordan vanlig modus aktiveres med egen nøkkel
  - hvor testdata, fasit, lagrede svar og resultattabell ligger
  - at automatiske tester ikke dokumenterer KI-kvalitet
  - kjente begrensninger
- **NFR-16 Hemmeligheter og ryddighet:** API-nøkkelen committes ikke. Repoet har en eksempelfil uten nøkkel. Testdata, fasit og lagrede svar ligger i egne mapper, adskilt fra applikasjonskoden.
- **NFR-17 Verifisering før innlevering:** Før innlevering følges README fra en ny klone på en maskin uten API-nøkkel. Det kontrolleres at installasjonen virker, at appen starter i demomodus, og at de automatiske testene består.

### 5.5 Generelle krav

- **NFR-18 API-nøkkel aldri i nettleseren:** API-nøkkelen er aldri tilgjengelig i nettleseren eller i kode som sendes til nettleseren. Den tekniske løsningen bestemmes i arkitekturfasen.
- **NFR-19 Språk:** Grensesnitt og resultater er på norsk bokmål.
- **NFR-20 Grunnleggende tilgjengelighet:** Kjerneflyten kan brukes med tastatur. Felt har synlige etiketter, og status formidles med tekst og ikke bare med farge. Designmålet for kontrast i kjerneflyten er minst 4,5:1 for vanlig tekst og minst 3:1 for stor tekst, og kontrastforholdet kontrolleres med et kontrastverktøy. PRD-en og dokumentasjonen påstår ikke samsvar med WCAG 2.1 AA uten at det faktisk er kontrollert.
- **NFR-21 Plattform:** Webapp som fungerer godt i oppdaterte nettlesere på datamaskin. Mobiltilpasning er ikke et MVP-krav.
- **NFR-22 Ventetid:** Analyser kan ta tid, så lasteindikator vises (FR-1, FR-11). Etter 60 sekunder uten svar behandles kallet som tidsavbrudd (FR-19). Grensen er foreløpig og kan justeres i implementeringsfasen dersom testing viser behov for det.
- **NFR-23 Prompts og KI-kall samlet:** Prompts og kall til AI-tjenesten samles på ett sted i koden, slik at modell og prompt kan byttes og evalueres samlet. Dette er tatt med fra briefen.

## 6. Non-Goals (Explicit)

- Appen er ikke en søkeordsoptimalisering for rekrutteringssystemer (ATS) og gir ingen samlet match-score. Den gir i stedet en konkret og etterprøvbar oversikt over annonsekrav, status og kildehenvisninger.
- Appen er ikke en generell chat. Den stiller ingen oppfølgingsspørsmål og tar ikke imot egne instruksjoner.
- Appen skriver aldri om kvalifikasjoner som ikke står i CV-teksten, heller ikke som forslag til hva brukeren «kunne ha».
- Appen er ikke en CV-bygger. Den lager ikke formatert CV og eksporterer ikke filer.
- Appen lagrer ikke brukerdata og har ingen kontoer.
- Appen lover ikke at brukeren får jobb eller intervju.
- PRD-en og appen er ikke en juridisk personvernvurdering.

## 7. MVP Scope

*Tre nivåer holdes adskilt: obligatoriske MVP-krav må være oppfylt, kvalitetsmål måles i evalueringen, og tilleggsmål og utvidelser skal ikke forsinke kjernefunksjonaliteten.*

### 7.1 Obligatoriske MVP-krav

- FR-1–FR-22.
- NFR-1–NFR-23, med unntak av det som er merket som tilleggsmål i 7.3.
- Testsett med T1–T5 som grunnsett og T6 som språkscenario, med separat kontrollert fasit.
- Lagrede svar for T1–T6 i demomodus.
- Automatiske tester med mock-data, gjennomført evaluering med resultattabell, og README.

### 7.2 Kvalitetsmål

Kvalitetsmålene for KI-svarene er definert i §8 og måles i evalueringen. At evalueringen er gjennomført og rapportert ærlig, er et MVP-krav. Resultatet av evalueringen rapporteres slik det er, også når et mål ikke er nådd.

### 7.3 Tilleggsmål

Gjøres bare hvis de ikke forsinker de obligatoriske MVP-kravene:
- varsel før brukeren forlater siden med innhold (FR-20)
- mobiltilpasning (NFR-21)
- kontrollert samsvar med WCAG 2.1 AA (NFR-20)

### 7.4 Utvidelser etter MVP

Vurderes først når kjerneflyten er implementert og har bestått de avtalte testene. De er ikke krav til MVP.
1. **Opplasting av CV som PDF eller DOCX**, med uttrekk av tekst som brukeren kan kontrollere før analysen.
2. **Flere søknadsversjoner i samme økt**, slik at brukeren kan lage og sammenligne søknadsutkast.

### 7.5 Utenfor scope

- **Senere muligheter, ikke forpliktelser:**
  - automatiske oppfølgingsspørsmål
  - PDF-eksport
  - ferdig formatert CV
  - lagrede brukerprofiler og innlogging
  - grensesnitt og søknad på engelsk
- Analyse av egen tekst uten API-nøkkel.

## 8. Success Metrics

*Målene gjelder evalueringen på det fiktive testsettet og de automatiske testene. De dokumenterer ikke tidsbesparelse, jobbintervjuer eller jobbresultater. Hver kjøring rapporteres for seg, per testkombinasjon. T1–T5 og T6 rapporteres hver for seg. Sjekklistepunktene viser til Product Brief.*

**Kritiske kvalitetsmål** *(må være oppfylt i alle kjøringer av alle testkombinasjoner for at evalueringen samlet skal regnes som bestått)*

- **SM-1 Ingen oppdiktede kvalifikasjoner:** 0 oppdiktede kvalifikasjoner i CV-forbedringsforslag og søknadsutkast. Sjekkliste punkt 4. Validerer FR-8 og FR-9.
- **SM-2 Ingen ugyldige kildehenvisninger i rått KI-svar:** 0 kildehenvisninger i rått KI-svar som ikke finnes ordrett i CV-teksten. Antallet applikasjonen fanget opp, rapporteres i tillegg. Sjekkliste punkt 2. Validerer FR-6.

**Øvrige kvalitetsmål** *(bestått eller ikke bestått rapporteres per kjøring og per testkombinasjon; hvordan de inngår i samlet bestått, er et åpent spørsmål, §9 spørsmål 2–3)*

- **SM-3 Uttrekk:** Alle annonsekrav i fasiten er funnet. Antall ekstra annonsekrav rapporteres. Sjekkliste punkt 1. Validerer FR-4.
- **SM-4 Status:** Statusen stemmer med fasiten for minst 80 % av de funne annonsekravene. Antallet annonsekrav klassifisert som *mangler* der fasiten sier *ikke oppgitt*, rapporteres i tillegg. Sjekkliste punkt 3. Validerer FR-5.
- **SM-5 Kravtype:** Andelen funne annonsekrav med riktig kravtype rapporteres. [ÅPENT SPØRSMÅL] Terskelen avklares før evalueringen kjøres (§9, spørsmål 1). Validerer FR-4.
- **SM-6 CV-forbedringsforslag:** Der fasiten viser et reelt forbedringsbehov, finnes et relevant og begrunnet CV-forbedringsforslag. Sjekkliste punkt 5. Validerer FR-8.
- **SM-7 Søknadsutkast:** Søknadsutkastet er på norsk, gjelder riktig stilling og kan redigeres og kopieres. Sjekkliste punkt 6. Validerer FR-9 og, for T6, FR-7.

**Funksjonalitet og leveranse**

- **SM-8 Automatiske tester:** Alle automatiske tester består uten API-nøkkel og uten nettverk. Validerer den funksjonelle delen av FR-1–FR-22. Dokumenterer funksjonalitet, ikke KI-kvalitet.
- **SM-9 Kjørbarhet:** Verifiseringen fra en ny klone (NFR-17) er gjennomført og bestått før innlevering. Validerer NFR-14–NFR-17.
- **SM-10 Kostnad:** Samlede API-kostnader rapporteres mot den foreløpige budsjettrammen (NFR-8).

**Motmål (skal ikke optimaliseres)**

- **SM-C1 Antall CV-forbedringsforslag:** Flere forslag er ikke bedre. Forslag uten reelt forbedringsbehov er støy. Motvekt til SM-6.
- **SM-C2 Andel annonsekrav med status dekket:** En høy andel ser bra ut, men kan bety at appen klassifiserer for mange annonsekrav som dekket. Motvekt til SM-4 og SM-2.
- **SM-C3 Beståtte mock-tester som mål på KI-kvalitet:** Mock-testene viser at koden virker, ikke at KI-svarene er riktige. Motvekt til SM-8.
- **SM-C4 Et overbevisende søknadsutkast:** En flytende tekst er ikke et mål hvis det går ut over faktagrunnlaget. Motvekt til SM-7, underordnet SM-1.
- **SM-C5 Beste kjøring eller gjennomsnitt:** Resultatet skal ikke se bedre ut ved å velge den beste kjøringen eller slå sammen kjøringer. Gjelder alle mål og de lagrede svarene i demomodus.

## 9. Open Questions

*Spørsmålene er ikke avklart og skal ikke behandles som beslutninger.*

| # | Spørsmål | Eier | Avklares |
|---|---|---|---|
| 1 | Terskel for riktig kravtype (SM-5). Product Brief har ingen. | Gruppen | Før evalueringen kjøres |
| 2 | Samlet bestått for øvrige kvalitetsmål (SM-3–SM-7) med tre kjøringer: Må alle sjekklistepunktene bestå i alle tre kjøringene, slik briefens regel per testkombinasjon tilsier, eller rapporteres de bare per kjøring? | Gruppen | Før evalueringen kjøres |
| 3 | Teller T6 med i samlet bestått, eller rapporteres T6 bare separat? De kritiske målene (SM-1, SM-2) gjelder T6 uansett. | Gruppen | Før evalueringen kjøres |
| 4 | Den foreløpige budsjettrammen på 200 kr (NFR-8) må bekreftes av gruppen. | Gruppen | Før modellvalg |
| 5 | Valg av AI-tjeneste og modell, vurdert mot NFR-2, NFR-3, NFR-5 og NFR-8. | Arkitekturfasen | I arkitekturen |
| 6 | De foreløpige lengdegrensene i FR-2 og FR-3 må kontrolleres mot testdataene og modellen. | Arkitektur og implementering | Når testdata og modell finnes |
| 7 | Skal det gjøres brukerutprøving med personer i målgruppen, slik Product Brief nevner som mulig? Det forutsettes ikke i PRD-en. | Gruppen | Etter at MVP-en virker |

## 10. Assumptions Index

*Antakelser som er bekreftet av gruppen 2026-11-05:*

- §2.3 UJ-2: Kjøretidsmiljøet README oppgir, er installert eller kan installeres gratis.
- FR-22: Bekreftelsen av informasjonen gjelder resten av økten, men lagres ikke permanent.
- NFR-22: Etter 60 sekunder uten svar behandles kallet som tidsavbrudd. Grensen er foreløpig og kan justeres i implementeringsfasen.
