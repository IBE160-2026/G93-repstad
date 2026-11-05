---
title: "AI CV & Job Application Assistant – produktbrief"
status: complete
created: 2026-09-26
updated: 2026-11-05
---

# AI CV & Job Application Assistant

## Executive Summary

AI CV & Job Application Assistant er en enkel webapplikasjon som hjelper nyutdannede med å tilpasse CV og jobbsøknad til konkrete stillingsannonser. Brukeren limer inn CV-tekst og en stillingsannonse. Appen viser for hvert krav i annonsen om det er dekket, ikke oppgitt eller mangler, med henvisning til teksten i CV-en. Deretter gir den konkrete forbedringsforslag til CV-en og et redigerbart søknadsutkast basert på brukerens faktiske bakgrunn.

Prosjektet gjennomføres i IBE160 Programmering med KI. Målet er en gjennomførbar MVP som kan testes systematisk, og som sensor kan kjøre lokalt uten API-nøkkel. Første versjon er på norsk og rettet mot jobbsøking i Norge. Brukeren kontrollerer og redigerer alltid resultatet før bruk.

## The Problem

En nyutdannet kan ha relevant utdanning, ferdigheter og arbeidserfaring, men være usikker på hvordan bakgrunnen bør presenteres for en bestemt stilling. En generell CV viser ikke nødvendigvis tydelig hvilke kvalifikasjoner som møter kravene i annonsen. Det kan derfor kreve mye arbeid å velge ut relevant informasjon og formulere en målrettet søknad.

Arbeidet kan gjøres manuelt eller med generelle AI-verktøy som ChatGPT. Da må brukeren selv forklare bakgrunnen sin, formulere instruksjoner og kontrollere at resultatet ikke inneholder påstander som ikke stemmer. Prosjektets behovshypotese er at en mer strukturert prosess kan redusere dette arbeidet. Behovet og forventet tidsbesparelse er foreløpig ikke bekreftet gjennom brukerundersøkelser.

## The Solution

Brukeren limer inn CV-tekst og teksten fra en stillingsannonse og starter analysen. Resultatet vises i tre deler:

1. **Kravanalyse.** Appen henter ut kravene i annonsen og gir hvert krav én status:
   - **Dekket:** CV-en inneholder opplysninger som oppfyller kravet. Den aktuelle teksten fra CV-en vises som kildehenvisning.
   - **Ikke oppgitt:** CV-en sier ingenting om kravet. Brukeren kan ha kompetansen, men har ikke skrevet den.
   - **Mangler:** CV-en inneholder opplysninger som viser at kravet ikke er oppfylt, for eksempel bachelorgrad der annonsen krever master.
2. **CV-forbedringsforslag.** Relevante og begrunnede forslag til hva som bør fremheves, omformuleres eller flyttes, der CV-en har et reelt forbedringsbehov. Hvert forslag knyttes til et annonsekrav og bygger bare på tekst som finnes i CV-en.
3. **Søknadsutkast.** Et utkast i et redigerbart tekstfelt som brukeren kan endre og kopiere.

Appen stiller ikke oppfølgingsspørsmål. Krav med status «ikke oppgitt» viser i stedet brukeren hvilke opplysninger som kan legges til i CV-en før en ny analyse. Forslag og utkast skal aldri inneholde utdanning, erfaring eller ferdigheter som ikke står i CV-en.

Er CV-en eller annonsen tom eller svært kort, viser appen en forståelig melding i stedet for et resultat.

**Demomodus:** Uten API-nøkkel starter appen i demomodus. Der velger brukeren én av de forhåndsdefinerte fiktive testkombinasjonene og får lagrede svar for den. Demomodus analyserer ikke vilkårlig innlimt tekst; det krever API-nøkkel. Demomodus er tydelig merket i grensesnittet, slik at sensor og andre kan prøve hele flyten uten konto, nøkkel eller kostnad.

## What Makes This Different

Den ønskede forskjellen fra en generell AI-chat er en fast arbeidsflyt for CV- og søknadstilpasning. Brukeren slipper å utforme egne AI-instruksjoner for hver stilling. Det finnes også egne CV-verktøy, som Teal og Jobscan, som sammenligner CV-er med stillingsannonser.

Dette prosjektet legger vekt på sporbarhet. Hvert krav får en eksplisitt status, «dekket» begrunnes med tekst fra CV-en, og det skilles mellom informasjon som ikke er oppgitt og kvalifikasjoner som mangler. Dette skal gjøre forslagene lettere å kontrollere. Prosjektet bygger ikke på en påstand om unik funksjonalitet eller dokumentert bedre resultater enn eksisterende verktøy.

## Who This Serves

Første versjon prioriterer nyutdannede som søker sin første relevante jobb i Norge. Den typiske brukeren har en generell CV og har funnet en interessant stillingsannonse, men trenger hjelp til å velge hvilke erfaringer og ferdigheter som bør fremheves.

For denne brukeren er ønsket resultat en oversikt over hvordan bakgrunnen møter annonsen, relevante CV-forbedringer og et brukbart søknadsutkast som krever mindre manuelt arbeid enn å starte fra bunnen av.

## Success Criteria

**Testsett.** Vi lager 5 fiktive CV-er (CV1–CV5) og 5 fiktive stillingsannonser (A1–A5) og setter sammen minst 5 faste testkombinasjoner som dekker ulike situasjoner:

| # | Kombinasjon | Situasjon |
|---|---|---|
| T1 | CV1 + A1 | God match: de fleste krav dekket |
| T2 | CV2 + A2 | Delvis match: blanding av dekket og ikke oppgitt |
| T3 | CV3 + A3 | Svak match: flere krav mangler |
| T4 | CV4 + A4 | Relevant erfaring formulert annerledes enn i annonsen |
| T5 | CV5 + A5 | Kort CV med lite informasjon |

For hver kombinasjon lager vi en **fasit** på forhånd: kravene i annonsen, forventet status for hvert krav og hvor CV-en har et reelt forbedringsbehov. Testdataene ligger i en egen mappe i repoet og inneholder bare fiktive personer.

**Sjekkliste per testkombinasjon:**

1. Alle krav i fasiten er med i kravanalysen, og hvert krav har én av statusene dekket, ikke oppgitt eller mangler.
2. Hvert krav med status «dekket» har en kildehenvisning, og teksten finnes ordrett i CV-en.
3. Klassifiseringen av annonsekravene stemmer med fasiten for minst 80 % av kravene. Grensen gjelder bare statusene dekket, ikke oppgitt og mangler.
4. Verken CV-forslag eller søknadsutkast inneholder utdanning, erfaring eller ferdigheter som ikke står i CV-en. Oppdiktede kvalifikasjoner aksepteres ikke i noen kombinasjon i testsettet.
5. Der fasiten viser et reelt forbedringsbehov, gir appen relevante og begrunnede forbedringsforslag knyttet til annonsekrav. Appen foreslår ikke endringer bare for å ha forslag.
6. Søknadsutkastet er på norsk, gjelder riktig stilling og kan redigeres og kopieres.

**Bestått / ikke bestått:**

- En kombinasjon er **bestått** når alle seks punktene er oppfylt. Ett oppdiktet element (punkt 4) eller én kildehenvisning som ikke finnes i CV-en (punkt 2) gir **ikke bestått**, uansett resten.
- Evalueringen er **bestått** når alle testkombinasjonene består med den valgte AI-tjenesten.
- Resultatene dokumenteres i en tabell i repoet, med dato og modell.

**Automatiske tester med mock-svar** (uten API-kall):

- Hele flyten, fra innliming til visning av kravanalyse, forslag og utkast, fungerer med lagrede svar.
- Tom eller svært kort CV eller annonse gir en forståelig melding i stedet for et resultat.
- Appen starter i demomodus når API-nøkkel mangler, og de forhåndsdefinerte testkombinasjonene gir lagrede svar.
- Kildehenvisninger som ikke finnes ordrett i CV-en blir oppdaget av koden.

Testene viser at kravene blir oppfylt i testsettet, men kan ikke bevise at AI-en aldri gjør feil. Personer i målgruppen kan prøve løsningen dersom det er praktisk mulig. Uten brukerutprøving vil konklusjoner om tidsbesparelse være begrensede.

## Scope

**MVP:**

- Norsk webapplikasjon med innliming av CV og stillingsannonse
- Kravanalyse med status dekket / ikke oppgitt / mangler og kildehenvisning til CV-teksten
- CV-forbedringsforslag knyttet til annonsekrav
- Redigerbart og kopierbart søknadsutkast
- Forståelige meldinger ved tom eller for kort input
- Demomodus med lagrede svar for forhåndsdefinerte fiktive testkombinasjoner når API-nøkkel mangler

**Utenfor MVP:** automatiske oppfølgingsspørsmål, analyse av vilkårlig tekst uten API-nøkkel, filopplasting, PDF-eksport, ferdig formatert CV, lagrede brukerprofiler, innlogging og engelsk språkstøtte.

**Personvern:** CV, annonse og resultater brukes bare i den aktuelle økten og lagres ikke i appen. CV-innhold skrives ikke til logger. I vanlig modus sendes CV-teksten til en ekstern AI-tjeneste, og grensesnittet informerer om det. Ved valg av AI-tjeneste dokumenteres hvordan tjenesten behandler data sendt via API-et. Utvikling, testing og demo bruker bare fiktive data.

**Kostnader:** AI-tjenesten velges med vekt på lav kostnad eller gratisnivå. Under utvikling og i automatiske tester brukes mock-svar, slik at reelle API-kall bare skjer ved manuell utprøving og den systematiske evalueringen. Lengden på innlimt tekst begrenses for å holde hvert kall lite.

**Kjørbarhet og repo:** Appen skal kunne startes lokalt etter README uten betalte kontoer. API-nøkkelen leses fra en `.env`-fil som ikke committes, og repoet inneholder en `.env.example`. Prompts og LLM-kall samles i én modul. Teknologistakk og konkret AI-tjeneste velges i arkitekturfasen.

## Vision

Ambisjonen er å gjøre det enklere for nyutdannede å presentere sin faktiske bakgrunn på en relevant og målrettet måte, samtidig som de beholder kontrollen over innholdet.

Første prioritet er en fungerende og testet kjerneflyt. Når den består testsettet, er disse utvidelsene prioritert:

1. **Opplasting av CV som PDF eller DOCX**, med uttrekk av tekst som brukeren kan kontrollere før analysen.
2. **Flere søknadsversjoner i økten**, slik at brukeren kan lage og sammenligne utkast for samme eller ulike annonser.

Senere muligheter er oppfølgingsspørsmål, PDF-eksport, lagrede profiler og engelsk språkstøtte. Dette er muligheter for videreutvikling, ikke forpliktelser.
