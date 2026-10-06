# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G93 – G93-repstad |
| **Product brief** | `_bmad-output/planning-artifacts/briefs/brief-AI CV & Job Application Assistant-2026-09-26/brief.md` (commit `c598365`) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Godt utgangspunkt med justeringer.** Gruppen kan gå videre og innarbeide punktene under.

Vi har vurdert `brief.md` for «AI CV & Job Application Assistant».

**Det som er bra:**

1. Briefen er nøktern, ærlig og godt avgrenset. Behovet er formulert som en «behovshypotese» som ikke er bekreftet. Dere hevder ikke unik funksjonalitet. Filopplasting, PDF-eksport, lagrede profiler og engelsk er tydelig utenfor MVP. Det er dessuten et godt personvernvalg at CV og annonse bare brukes i økten og ikke lagres.
2. Kvalitetskravene til KI-delen er gjennomtenkte. Dere skiller mellom informasjon som ikke er oppgitt og kvalifikasjoner brukeren ikke har, påstander skal kunne spores til oppgitte opplysninger, og evalueringen skal gjøres med fiktive CV-er og annonser. Dere er også ærlige om at «en enkel evaluering kan ikke bevise at AI-en aldri gjør feil».

**De viktigste endringene:**

1. Suksesskriteriene (relevans, faktagrunnlag og brukbarhet) er gode prinsipper, men må gjøres konkrete nok til å bli testtilfeller. Bestem antall testeksempler og hva som skal sjekkes for hvert av dem nå. Ikke utsett det.
2. Omfanget er smalt. Kjerneflyten kan bli ferdig ganske raskt, og da blir det lite å vise i funksjonalitet og testing. Planlegg én eller to tydelige utvidelser som kan tas når kjernen virker.
3. «Appen kan ved behov stille oppfølgingsspørsmål» er en dialogfunksjon som gjør flyten mer kompleks. Beskriv når det skjer, og hvordan svaret brukes, eller flytt funksjonen til en senere utvidelse.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Enkel**

**Sammenlignbart med:** 2) AI CV- og søknadsassistent (middels), men avgrenset. Uten filopplasting, kontoer og lagring ligger v1 nærmere 8) Foredragsnotater → sammendrag og quizgenerator (enkel): innlimt tekst inn, KI-generert tekst ut. Kravene til sporbarhet og ingen oppdiktede kvalifikasjoner gjør den likevel noe mer krevende enn de enkleste variantene.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | lav | Lite regelbasert logikk. Koblingen mellom annonsekrav og bakgrunn gjøres i hovedsak av språkmodellen. |
| Datamodell – antall entiteter og relasjoner mellom dem | lav | CV-tekst, annonsetekst og resultater i én økt. Ingen lagring. |
| Brukere, roller og innlogging | lav | Ingen innlogging eller roller. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | middels | Analyse av koblinger og mangler, CV-forslag og søknadsutkast, med krav om sporbarhet og ingen oppdikting. Oppfølgingsspørsmål gir en ekstra dialogrunde. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | middels | Én ekstern AI-tjeneste. Ikke valgt ennå. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | lav | Ingen. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | lav | Bevisst utelatt. Bare innliming og kopiering. |
| Sikkerhet og personvern | middels | CV-tekst med personopplysninger sendes til en ekstern AI-tjeneste. Det er bra at dere nevner det. Beskriv valget når tjenesten er bestemt. |

**Hva vanskelighetsgraden betyr for dere:**

- _Enkel:_ Et enkelt prosjekt gir stor sjanse for å bli ferdig. Vanskelighetsgraden inngår likevel i vurderingen, så for å nå helt opp må dere vise mer i gjennomføringen. Det betyr særlig et gjennomarbeidet design, grundig testing, en tydelig dokumentert prosess og en README som virker. Den systematiske evalueringen med fiktive CV-er som dere allerede har planlagt, er et godt sted å vise kvalitet.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | OK | Godt innenfor rekkevidde for én person. Faren er heller for lite enn for mye omfang. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | OK | Flyten er tydelig. PRD-en må presisere oppfølgingsspørsmålene og hvordan koblingene vises. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | En enkel webapp med ett LLM-kall per steg er godt egnet. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | OK | Med fiktive CV-er der dere vet nøyaktig hva som står, kan dere kontrollere om forslag inneholder noe som ikke finnes i CV-en. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | risiko | Flyten kan testes automatisk med mock-svar. KI-kvaliteten må testes med et fast testsett og en sjekkliste, og terskler og antall eksempler er ikke bestemt ennå. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | risiko | Ikke omtalt. Planlegg en demomodus med lagrede svar for en fiktiv CV og annonse når nøkkel mangler. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | risiko | AI-tjeneste er ikke valgt. Velg en med lav kostnad eller gratisnivå, og bruk mock-svar under utvikling. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart som beskrevet.**

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Gjør sporbarheten synlig i grensesnittet. Vis for hvert annonsekrav om det er «dekket», «ikke oppgitt» eller «mangler», med henvisning til linjen i CV-en som dekker det. Det gir en strukturert funksjon som kan testes, og styrker kjernen i det dere vil oppnå.
2. Ha en utvidelse klar når kjernen virker, for eksempel filopplasting av CV (PDF/DOCX) eller lagring av flere søknadsversjoner i økten, slik at dere har mer å vise i funksjonalitet og testing.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Klart: lim inn CV og annonse, få CV-forslag og søknadsutkast basert på faktisk bakgrunn. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Konkret om nyutdannede som er usikre på hva som bør fremheves, og ærlig om at behovet ikke er bekreftet. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | Juster | Godt beskrevet fra brukerens side. Presiser oppfølgingsspørsmålene og hvordan «relevante koblinger» vises. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Ærlig: fast arbeidsflyt i stedet for egne instruksjoner til en generell chat, uten påstand om unikhet. Dere kan gjerne nevne eksisterende CV-verktøy (for eksempel Teal eller Jobscan) i tillegg til ChatGPT. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Én tydelig primærbruker: nyutdannede som søker første relevante jobb i Norge. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | Gode prinsipper og en god evalueringsmetode. Gjør dem konkrete, for eksempel «for 5 fiktive CV-er og 5 annonser inneholder ingen forslag utdanning, erfaring eller ferdigheter som ikke står i CV-en», «alle krav i annonsen er markert som dekket, ikke oppgitt eller mangler» og «tom eller svært kort CV gir en forståelig melding i stedet for et utkast». |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | OK | Tydelig hva som er med og ikke. Plasser oppfølgingsspørsmålene enten i eller utenfor MVP. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Utvidelsene er tydelig merket som muligheter, ikke forpliktelser. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | OK | Briefen er presis og ligger i BMAD-strukturen. Fortsett med PRD og små, beskrivende commits. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Juster | Kjerneflyten er tydelig og realistisk, men smal. Planlegg en utvidelse, slik at det blir nok funksjonalitet å vise. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Juster | Evalueringsopplegget er et godt utgangspunkt. Bestem testsett og sjekkliste nå, og kombiner med automatiske tester med mock-svar. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | Juster | Brukeren er tydelig. Skisser hvordan koblinger, mangler og utkast presenteres, slik at resultatet blir oversiktlig og lett å redigere. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Teknologi er ikke valgt ennå. Hold det enkelt, og samle prompts og LLM-kall i én modul. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Juster | Planlegg demomodus eller mock-svar uten nøkkel, og legg ved fiktive eksempel-CV-er og annonser. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Legg de fiktive testdataene i en egen mappe, og hold API-nøkkelen i `.env` som ikke committes. |

## 3. Neste steg for gruppen

1. Gjør suksesskriteriene konkrete: antall testeksempler, sjekkliste per eksempel og hva som regnes som godkjent.
2. Avklar oppfølgingsspørsmålene (inn eller ut av MVP), og beskriv hvordan koblinger og mangler skal vises.
3. Legg til en planlagt utvidelse og en plan for demomodus uten nøkkel, og gå videre til PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
