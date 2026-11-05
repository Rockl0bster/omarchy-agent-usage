# Plan: valgfri kompakt visning i Agent Usage

## Mål

Gi brukeren en innstilling som skjuler tekstnavnene «Claude» og «Codex» i topplinjen for å spare plass. Ikoner, forbrukstall og tid til nullstilling skal fortsatt vises. Navnene i detaljpanelet beholdes.

## Avgrensning

- Én felles av/på-innstilling, for eksempel «Show provider names in bar», i pluginens eksisterende innstillingsgrensesnitt.
- Navn vises som standard, slik at eksisterende brukere får samme utseende etter oppdatering.
- Ingen endringer i innsamling av data, innlogging, oppdateringsintervall eller beregning av forbruk.
- Ingen installasjon eller endring av brukerens aktive plugin før kodegjennomgang og uttrykkelig klarsignal til testing.

## Teknisk forslag

1. Kontroller oppdatert upstream-kode og Omarchys gjeldende støtte for boolske plugininnstillinger og grensesnittet som viser dem.
2. Legg til en boolsk innstilling med standardverdi `true` i `manifest.json`, med et navn som passer prosjektets konvensjoner.
3. Bruk innstillingen i `ProviderChip` i `Panel.qml` til å skjule bare navnet i topplinjen. Sørg for at både tekstbredden og eventuell ekstra avstand forsvinner. Ikoner, prosent, nedtelling og farger skal fungere som før.
4. Behold navn i detaljpanelet og sørg for at de fortsatt er tilgjengelige for brukere som trenger dem; vurder tilgjengelighetsmerking eller beskrivende verktøytips i tråd med eksisterende komponenter.
5. Dokumenter innstillingen og hvordan den brukes i `README.md`. Unngå andre funksjonsendringer.

Dette er et forslag som kan justeres etter gjennomgang av oppdatert kode og rammeverk. Endringen skal være liten og egnet for originalprosjektet.

## Gjennomgang og testing

1. Lag kodeendringen i en egen gren basert på oppdatert upstream, atskilt fra denne plangrenen. Del diffen for gjennomgang med flere modeller før lokal installasjon eller kjøring.
2. Gjennomgå innstillingens standardverdi, persistens og kompatibilitet med eksisterende konfigurasjon. Kontroller at navn i detaljpanelet beholdes.
3. Etter brukerens klarsignal: test på maskinen med navn både på og av. Kontroller faktisk bredde, begge ikonene, prosent, nedtelling, farger, klikk på detaljpanelet og oppførsel når data mangler. Kontroller at innstillingen overlever omstart av shell eller innlogging.
4. Kjør prosjektets relevante automatiske kontroller der de finnes, og dokumenter resultatene. Planlegg en enkel tilbakeføring til den installerte originalversjonen før testing.
5. Når brukeren har godkjent resultatet, opprett en pull request mot originalprosjektet med forklaring, skjermbilder ved behov og testresultater. Eierne avgjør om endringen flettes inn.

## Git-arbeidsflyt

Denne planen ligger på en egen gren i forken. En senere kodegren opprettes fra upstreams standardgren, slik at `plan.md` ikke automatisk følger med i pull requesten. Ingen pull request opprettes som del av denne planleggingsoppgaven. Når endringen eventuelt er flettet inn upstream, kan den offisielle pluginen brukes videre uten å vedlikeholde en egen fork, forutsatt at oppdateringen installeres.
