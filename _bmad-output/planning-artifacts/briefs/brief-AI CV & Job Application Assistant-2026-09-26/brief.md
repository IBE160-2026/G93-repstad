---
title: "AI CV & Job Application Assistant – produktbrief"
status: complete
created: 2026-09-26
updated: 2026-09-26
---

# AI CV & Job Application Assistant

## Executive Summary

AI CV & Job Application Assistant er en enkel webapplikasjon som skal hjelpe nyutdannede med å tilpasse CV og jobbsøknad til konkrete stillingsannonser. Brukeren limer inn en eksisterende CV og en stillingsannonse og får konkrete forbedringsforslag til CV-en og et søknadsutkast basert på sin faktiske bakgrunn.

Prosjektet gjennomføres i IBE160 Programmering med KI. Målet er en gjennomførbar MVP som gjør tilpasningsarbeidet enklere og mer strukturert. Første versjon er på norsk og rettet mot jobbsøking i Norge. Brukeren skal alltid kunne kontrollere og redigere resultatet før bruk.

## The Problem

En nyutdannet kan ha relevant utdanning, ferdigheter og arbeidserfaring, men være usikker på hvordan bakgrunnen bør presenteres for en bestemt stilling. En generell CV viser ikke nødvendigvis tydelig hvilke kvalifikasjoner som møter kravene i annonsen. Det kan derfor kreve mye arbeid å velge ut relevant informasjon og formulere en målrettet søknad.

Arbeidet kan gjøres manuelt eller med generelle AI-verktøy som ChatGPT. Da må brukeren selv forklare bakgrunnen sin, formulere instruksjoner og bearbeide resultatet. Prosjektets behovshypotese er at en mer strukturert prosess kan redusere dette arbeidet. Behovet og forventet tidsbesparelse er foreløpig ikke bekreftet gjennom brukerundersøkelser.

## The Solution

Brukeren limer inn CV-tekst og teksten fra en stillingsannonse. Appen sammenholder annonsekravene med oppgitt utdanning, erfaring og kompetanse, og viser hvilke deler av bakgrunnen som er relevante. Deretter gir den konkrete CV-forbedringsforslag og et utkast til en tilpasset jobbsøknad.

Manglende opplysninger skal synliggjøres, og appen kan ved behov stille oppfølgingsspørsmål. Den skal skille mellom informasjon som ikke er oppgitt, og kvalifikasjoner brukeren faktisk ikke har. Forslagene skal ikke inneholde oppdiktet utdanning, erfaring eller kompetanse.

Resultatene vises som tekst som brukeren kan kontrollere, redigere og kopiere. Brukeren har alltid siste kontroll over innholdet.

## What Makes This Different

Den ønskede forskjellen fra en generell AI-chat er en fast arbeidsflyt for CV- og søknadstilpasning. Brukeren legger inn CV og annonse uten å måtte utforme egne AI-instruksjoner for hver stilling.

Løsningen skal vise koblingen mellom faktisk bakgrunn og annonsekrav og gjøre manglende informasjon tydelig. Dette skal hjelpe brukeren med å forstå og kontrollere forslagene. Prosjektet bygger ikke på en påstand om unik funksjonalitet eller dokumentert bedre resultater enn eksisterende verktøy.

## Who This Serves

Første versjon prioriterer nyutdannede som søker sin første relevante jobb i Norge. Den typiske brukeren har en generell CV og har funnet en interessant stillingsannonse, men trenger hjelp til å velge hvilke erfaringer og ferdigheter som bør fremheves.

For denne brukeren er ønsket resultat relevante CV-forbedringer og et brukbart søknadsutkast som krever mindre manuelt arbeid enn å starte fra bunnen av.

## Success Criteria

Løsningen skal vurderes ut fra tre kriterier:

- **Relevans:** Forslagene kobler brukerens faktiske utdanning, erfaring og kompetanse til kravene i stillingsannonsen.
- **Faktagrunnlag:** Påstander om brukeren kan spores til oppgitte opplysninger. Manglende informasjon håndteres uten oppdiktede kvalifikasjoner.
- **Brukbarhet:** CV-forslagene og søknadsutkastet gir et nyttig grunnlag som brukeren kan redigere videre.

Evalueringen gjennomføres med fiktive CV-er og forskjellige fiktive stillingsannonser. Forslagenes relevans, faktagrunnlag og behov for redigering kontrolleres for hvert eksempel. Personer i målgruppen kan også prøve løsningen dersom det er praktisk mulig.

Mindre manuelt arbeid er et ønsket resultat, men konklusjoner om tidsbesparelse vil være begrensede uten brukerutprøving. Kravet om ingen oppdiktede kvalifikasjoner skal testes; en enkel evaluering kan ikke bevise at AI-en aldri gjør feil.

## Scope

MVP-en omfatter en norsk webapplikasjon med innliming av CV og stillingsannonse, sammenligning av innholdet, synliggjøring av relevante koblinger og manglende opplysninger, CV-forbedringsforslag og et redigerbart og kopierbart søknadsutkast.

Første versjon skal ikke produsere en ferdig formatert CV. Filopplasting, PDF-eksport, lagrede brukerprofiler og engelsk språkstøtte ligger utenfor MVP-en.

CV, stillingsannonse og genererte søknader skal brukes i den aktuelle økten og ikke lagres i appen for senere bruk. Personvern og eventuell behandling eller lagring hos en ekstern AI-tjeneste må vurderes ved teknologivalg.

Teknologistakk og AI-tjeneste er ikke valgt. Konkret tidsplan, antall testeksempler og eventuelle terskler for godkjent evaluering må tilpasses studentprosjektets begrensede rammer.

## Vision

Ambisjonen er å gjøre det enklere for nyutdannede å presentere sin faktiske bakgrunn på en relevant og målrettet måte, samtidig som de beholder kontrollen over innholdet.

Første prioritet er en fungerende kjerneprosess. Dersom tid og behov tilsier det, kan løsningen senere utvides med filopplasting, PDF-eksport, lagrede profiler eller engelsk språkstøtte. Dette er muligheter for videreutvikling, ikke forpliktelser i første versjon.
