# Internetconnectiviteit assessment

**Status:** Huidige voorkeurskeuze  
**Datum:** 2026-08-17

## Context

Deze beoordeling vertaalt de gewenste internetconnectiviteit van Falkor naar een concrete productvoorkeur. Dit document heeft geen normatief karakter en legt geen architectuurbesluiten vast.

De behoefte is primair ontstaan vanuit de wens om de Cerbo GX permanent bereikbaar te houden voor monitoring op afstand via VRM, onafhankelijk van de beschikbaarheid van havenwifi.

Daarnaast is het wenselijk dat dezelfde oplossing een lokaal wifi-netwerk kan aanbieden voor algemeen gebruik aan boord, waaronder internettoegang voor telefoons, tablets, laptops en incidenteel thuiswerken.

Deze assessment beoordeelt beschikbare oplossingen tegen deze behoefte.

## Architecturale uitgangspunten

- Monitoring van de energievoorziening moet onafhankelijk zijn van haveninfrastructuur.
- De oplossing moet direct kunnen werken op het 12V-boordnet.
- De oplossing moet permanent operationeel kunnen blijven.
- De oplossing moet eenvoudig uitbreidbaar zijn voor algemeen netwerkgebruik aan boord.
- Voorkeur voor een beperkt aantal componenten.

## Architecturale requirements

### Permanente verbinding voor Cerbo GX

De Cerbo GX moet permanent verbinding kunnen maken met VRM, ook wanneer Falkor onbeheerd in een haven ligt.

### Onafhankelijkheid van havenwifi

De monitoringfunctionaliteit mag niet afhankelijk zijn van beschikbaarheid, kwaliteit of wijzigingen van havenwifi.

### Directe aansluiting op 12V

De oplossing moet rechtstreeks kunnen worden aangesloten op het 12V-boordnet zonder aanvullende omvormers.

### Ondersteuning lokaal netwerk

Het is wenselijk dat dezelfde oplossing tevens een lokaal netwerk beschikbaar maakt voor apparaten aan boord.

### Lage beheerlast

De oplossing moet zonder frequente handmatige handelingen operationeel kunnen blijven.

### Uitbreidbaarheid

Toekomstige uitbreiding met aanvullende netwerkapparatuur moet mogelijk zijn zonder vervanging van de gekozen oplossing.

## Kandidaatoplossingen

### Victron GX LTE 4G

**Prijsindicatie:** € 200  
**Architecturale fit:** Middel

**Sterke punten:**

- Specifiek ontworpen voor GX-apparaten.
- Eenvoudige configuratie.
- Laag stroomverbruik.
- Directe integratie met het Victron-ecosysteem.
- Vult de primaire requirement volledig in.

**Aandachtspunten:**

- Geen volwaardige routerfunctionaliteit.
- Geen centraal wifi-netwerk voor de boot.
- Internetgebruik door bemanning vereist aanvullende apparatuur.
- Beperkte uitbreidbaarheid buiten de Cerbo-use-case.

### Teltonika RUTM11

**Prijsindicatie:** € 300  
**Architecturale fit:** Hoog

**Sterke punten:**

- Direct geschikt voor aansluiting op het 12V-boordnet.
- Ondersteunt permanente verbinding voor de Cerbo GX.
- Biedt een centraal wifi-netwerk voor de gehele boot.
- Ethernetpoorten beschikbaar voor vaste netwerkverbindingen.
- Cerbo GX kan bekabeld worden aangesloten.
- Ondersteunt dual-SIM configuraties.
- Eenvoudig uitbreidbaar voor toekomstige netwerkbehoeften.
- Eén oplossing voor zowel monitoring als algemeen internetgebruik.

**Aandachtspunten:**

- Meer functionaliteit dan strikt noodzakelijk voor uitsluitend VRM-monitoring.
- Hoger stroomverbruik dan een dedicated GX-modem.
- Meer configuratiemogelijkheden dan voor de primaire use-case noodzakelijk zijn.

### Mobiele hotspot

**Prijsindicatie:** € 50 - € 150  
**Architecturale fit:** Laag

**Sterke punten:**

- Lage aanschafkosten.
- Eenvoudig in gebruik.

**Aandachtspunten:**

- Veel modellen zijn gebaseerd op een interne accu.
- Minder geschikt voor permanente installatie.
- Beperkte uitbreidbaarheid.
- Minder robuust voor continu gebruik.
- Cerbo-monitoring wordt afhankelijk van consumentenelektronica.

### Afgevallen selectiecriteria

### 5G

Voor de geïdentificeerde use-cases is geen expliciete behoefte vastgesteld die uitsluitend door 5G kan worden ingevuld.

### Externe LTE-antennes

Voor het huidige operationele profiel is geen concrete noodzaak vastgesteld voor externe LTE-antennes. De verwachting is dat internetgebruik voornamelijk plaatsvindt in havens met voldoende mobiele dekking.

### Hoge doorvoersnelheid

De primaire use-case betreft monitoring van de Cerbo GX. Doorvoersnelheid vormt daarom geen zelfstandig selectiecriterium.

### Onbeperkte databundels

De keuze van abonnementen valt buiten de scope van deze assessment en kan onafhankelijk van de gekozen hardware worden aangepast.

## Netwerkarchitectuur

### Configuratie A

- GX LTE 4G rechtstreeks gekoppeld aan Cerbo GX.

**Voordelen:**

- Eenvoudig.
- Laag stroomverbruik.
- Vervult de primaire monitoringbehoefte.

**Nadelen:**

- Geen wifi-netwerk voor algemeen gebruik.
- Tweede oplossing nodig voor internettoegang aan boord.

### Configuratie B

- RUTM11.
- Cerbo GX via Ethernet.
- Wifi voor bemanning.

**Voordelen:**

- Eén geïntegreerde oplossing.
- Onafhankelijke Cerbo-connectiviteit.
- Centrale netwerkvoorziening voor de boot.
- Ondersteunt zowel huidige als toekomstige use-cases.

**Nadelen:**

- Meer functionaliteit dan strikt noodzakelijk voor monitoring.

## Huidige voorkeurskeuze

### 1. Teltonika RUTM11

**Beoordeling:** Voorkeursoplossing

De RUTM11 biedt de beste balans tussen de primaire requirement van permanente Cerbo-connectiviteit en de secundaire wens om een bruikbaar netwerk aan boord beschikbaar te maken.

De oplossing ondersteunt zowel monitoring op afstand als algemeen internetgebruik zonder aanvullende apparatuur.

### 2. Victron GX LTE 4G

**Beoordeling:** Functioneel passend, beperkt toepassingsgebied

De GX LTE 4G sluit uitstekend aan op de monitoringbehoefte, maar creëert geen generieke netwerkvoorziening voor overige apparatuur aan boord.

### 3. Mobiele hotspot

**Beoordeling:** Niet aanbevolen als primaire oplossing

Een mobiele hotspot kan functioneel voldoen, maar sluit minder goed aan op de wens voor een permanente, geïntegreerde en onderhoudsarme installatie.

## Open punten

- Bepalen welk type mobiele databundel het beste aansluit bij het daadwerkelijke gebruikspatroon.
- Valideren of dual-SIM daadwerkelijk meerwaarde biedt ten opzichte van een enkele SIM-kaart.
- Valideren of een externe LTE-antenne noodzakelijk blijkt op basis van praktijkervaring.

## Herbeoordeling

Deze keuze dient opnieuw beoordeeld te worden:

- bij significante prijswijzigingen;
- bij introductie van nieuwe producten;
- bij wijziging van operationele requirements;
- wanneer structureel remote gewerkt wordt vanaf Falkor;
- voorafgaand aan daadwerkelijke aanschaf.
