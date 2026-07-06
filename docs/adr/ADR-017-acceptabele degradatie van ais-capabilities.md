# ADR-017 — Acceptabele degradatie van AIS-capabilities

**Status:** Geaccepteerd  
**Datum:** 2026-07-06

## Context en probleemstelling

Binnen de target-architectuur vervult AIS meerdere functies. Enerzijds ondersteunt AIS het beoordelen van de verkeerssituatie rondom Falkor. Anderzijds ondersteunt AIS het beoordelen van deze verkeerssituatie in geografische context. Deze capabilities zijn uitgewerkt in ADR-016.

Uitval van componenten zoals displays, datadistributie, AIS-apparatuur of voedingsvoorzieningen kan leiden tot verlies van functionaliteit. Niet iedere vorm van degradatie heeft dezelfde operationele impact en niet iedere vorm van degradatie rechtvaardigt aanvullende mitigaties.

De vraag is welke degradatie van AIS-capabilities binnen de target-architectuur acceptabel wordt geacht.

## Beslissingscriteria

- Ondersteuning van veilige navigatie.
- Ondersteuning van de in ADR-016 beschreven capabilities.
- Kans op optreden van het uitvalscenario.
- Operationele impact van het uitvalscenario.
- Beheersbare complexiteit.
- Verhouding tussen risico en mitigatiekosten.
- Aansluiting bij het operationeel profiel van Falkor (ADR-019).

## Overwogen opties

### Optie A — Geaccepteerde degradatie (gekozen)

De architectuur accepteert dat uitval van individuele componenten kan leiden tot gedeeltelijk of volledig verlies van AIS-functionaliteit. Voor specifieke uitvalscenario's worden geen aanvullende mitigatiemaatregelen getroffen wanneer de kans, impact en operationele context dit niet rechtvaardigen.

**Voordelen:**

- Eenvoudige architectuur.
- Lage complexiteit.
- Lage kosten.
- Geen aanvullende componenten uitsluitend voor redundantie.
- Voorkomt over-engineering van laag-risicoscenario's.

**Nadelen:**

- Sommige uitvalscenario's leiden direct tot verlies van AIS-functionaliteit.
- Minder operationele mogelijkheden tijdens degradatiescenario's.
- Beperkte bescherming tegen enkelvoudige faalpunten.

### Optie B — Behoud van verkeerssituatie rondom Falkor

De capability om de verkeerssituatie rondom Falkor te beoordelen wordt expliciet beschermd tegen uitval van een enkele gebruikersinterface. Uitval van een individuele gebruikersinterface mag niet leiden tot verlies van deze capability.

**Voordelen:**

- Beschermt de operationeel belangrijkste AIS-capability.
- Beperkte extra complexiteit.
- Goede aansluiting bij kustvaart en drukke vaargebieden.

**Nadelen:**

- Vereist aanvullende gebruikersinterfaces of presentatiepaden.
- Introduceert aanvullende complexiteit in de presentatiearchitectuur.
- Niet alle AIS-functionaliteit blijft noodzakelijk beschikbaar.

### Optie C — Behoud van alle AIS-capabilities

De architectuur richt zich op behoud van zowel verkeerssituatie rondom Falkor als geografische context bij uitval van individuele componenten.

**Voordelen:**

- Maximale beschikbaarheid van AIS-functionaliteit.

**Nadelen:**

- Hoge complexiteit.
- Hogere kosten.
- Meer afhankelijkheden en functionele overlap.
- Lastiger te rechtvaardigen voor het operationeel profiel van Falkor (ADR-019).

## Risicoscenario's

### Uitval van een gebruikersinterface

Voorbeelden:

- plotter defect;
- instrumentdisplay defect;
- marifoon defect.

Mogelijke gevolgen:

- verlies van verkeerssituatie rondom Falkor;
- verlies van geografische context;
- verlies van beide capabilities.

**Beoordeling:**

De wens voor meerdere gebruikersinterfaces wordt primair gedreven door algemene HMI-overwegingen en niet door AIS-specifieke eisen.

### Uitval van AIS-datadistributie

Voorbeelden:

- storing in NMEA 2000;
- verlies van netwerkvoeding.

Mogelijke gevolgen:

- AIS-informatie bereikt geen gebruikersinterfaces meer.

**Beoordeling:**

Dit wordt beschouwd als een generiek dataplatformrisico. De impact raakt niet alleen AIS, maar ook andere informatie zoals GPS-, diepte-, log- en windgegevens.

### Uitval van AIS-transponder

Voorbeelden:

- hardwaredefect;
- verlies van voedingsspanning.

Mogelijke gevolgen:

- verlies van AIS-transmissie;
- verlies van AIS-ontvangst via de primaire AIS-bron.

Alternatieve zichtbaarheid van Falkor blijft mogelijk via:

- radarreflector;
- navigatieverlichting;
- marifoon;
- visuele waarneming.

**Beoordeling:**

De kans op uitval wordt als laag beschouwd. Aanvullende mitigatie vereist substantiële functionele overlap en wordt daarom niet proportioneel geacht.

## Besluit

De target-architectuur kent geen expliciete redundantie-eisen voor AIS-transmissie of AIS-datadistributie.

Uitval van een AIS-transponder wordt geaccepteerd als een laag-kansscenario waarvoor aanvullende mitigatie niet proportioneel wordt geacht.Uitval van NMEA 2000 wordt behandeld als een generiek dataplatformrisico en niet als een AIS-specifiek risico.Voor gebruikersinterfaces geldt dat verlies van één display niet automatisch mag leiden tot verlies van alle operationeel relevante informatie. Deze eis wordt echter niet uitsluitend door AIS gedreven en wordt binnen de bredere display- en HMI-architectuur beschouwd.

Acceptatie van degradatie heeft de voorkeur boven toevoeging van AIS-specifieke redundantie wanneer de kans op optreden laag is en alternatieve veiligheidsmaatregelen beschikbaar blijven.

## Gevolgen

### Positief

- Geen AIS-specifieke redundantie vereist.
- Lage architecturale complexiteit.
- Lage kosten.
- Geen aanvullende AIS-componenten uitsluitend voor mitigatie van laag-risicoscenario's.
- Duidelijke afweging tussen risico en mitigatie.

### Negatief

- Uitval van een AIS-transponder leidt direct tot verlies van AIS-transmissie.
- Uitval van een AIS-transponder leidt direct tot verlies van AIS-ontvangst via de primaire AIS-bron.
- Sommige degradatiescenario's worden expliciet geaccepteerd.
- Bescherming tegen enkelvoudige faalpunten wordt niet specifiek voor AIS afgedwongen.
