# helsearbeidsgiver-pdfgen

Generering av PDF-dokumenter for helsearbeidsgiver-tjenester (f.eks.sykmelding for arbeidsgiver).

## Getting started
Kjør følgende (krever docker på maskinen)  

```
docker login ghcr.io --username [github brukernavn]
(lim in PAT med read:packages tilgang som passord)

chmod +x run_development.sh
./run_development.sh
```  
Serveren blir startet.  
Åpne opp den relevante PDF url i nettleseren.  
F.eks: http://0.0.0.0:8080/api/v1/genpdf/sykmelding/sykmelding

Alle endringer til templates osv. blir nå reflektert i nettleseren ved refresh uten å restarte serveren.

## Utvikling av PDF
PDF-dokumentene genereres fra [Typst](https://typst.app/)-maler (`.typ`) i `templates`-mappen av [pdfgenrs](https://github.com/navikt/pdfgenrs). Testdata for lokal utvikling ligger i `data`-mappen. Endringer i maler, data, fonter eller ressurser krever omstart av utviklingsserveren.

## Tester
Tester er implementert med Kotlin og TestContainers.

Dette betyr at Dockerfilen blir kjørt og systemet er testet end-to-end.

Testene henter .json filer fra `src/test/resources/` og lagrer PDF filene i `build/test-pdf/` med samme navn. 

## pdfgenrs

Dette repoet implementerer pdfgenrs, se på [pdfgenrs-repoet](https://github.com/navikt/pdfgenrs) for mer informasjon.

Dockerfilen som bygges bruker bare disse 3 mappene fra dette repoet:

```Docker
FROM ghcr.io/navikt/pdfgenrs:xxx

COPY templates /app/templates
COPY fonts /app/fonts
COPY resources /app/resources
COPY data /app/data
```

Et eksempel på et pdfgenrs-basert prosjekt er [pdfgenrs-test](https://github.com/navikt/pdfgenrs-test).

## For NAV-ansatte

Interne henvendelser kan sendes via Slack i kanalen #helse-arbeidsgiver.
