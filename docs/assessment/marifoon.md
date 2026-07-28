# Marifoon assessment

**Status:** Huidige voorkeurskeuze  
**Datum:** 2026-07-28

## Context

Deze beoordeling vertaalt de vastgestelde architectuur naar een concrete productvoorkeur. Dit document heeft geen normatief karakter en legt geen architectuurbesluiten vast.

ADR-020 bepaalt dat de target-architectuur uitgaat van een black-box marifoonarchitectuur waarbij de primaire bediening zich in de kuip bevindt en de radio-unit onafhankelijk van de gebruikersinterface wordt opgesteld.

Deze assessment beoordeelt beschikbare producten tegen deze vastgestelde architectuur.

## Architecturale uitgangspunten

- ADR-006 — NMEA2000 modelleren als één logisch netwerk
- ADR-014 — Platformkeuze voor data
- ADR-015 — AIS-transmissietechnologie
- ADR-016 — Eisen aan presentatie van AIS-informatie
- ADR-017 — Acceptabele degradatie van AIS-capabilities
- ADR-018 — Antennearchitectuur voor VHF en AIS
- ADR-019 — Operationeel profiel van Falkor
- ADR-020 — Architectuur van marifoonbediening

## Architecturale requirements

### Primaire bediening vanuit de kuip

De wachtvoerder moet de marifoon volledig kunnen bedienen vanaf de primaire operationele werkplek.

### Radio-unit beschermd opgesteld

De radio-unit moet binnen en beschermd tegen weersinvloeden kunnen worden geplaatst.

### Consistente bediening

De architectuur heeft voorkeur voor identieke gebruikersinterfaces op verschillende bedieningslocaties.

### NMEA 2000 integratie

De marifoon moet kunnen deelnemen aan het NMEA 2000 dataplatform.

### Ondersteuning binnenwater en zee

De marifoon moet geschikt zijn voor gebruik op zowel binnenwater als zee.

### Fallback-bediening

Bediening vanuit de kaartentafel is wenselijk als fallback-capability, maar vormt geen primaire requirement.

## Kandidaatoplossingen

### Icom IC-M410BB

**Prijsindicatie:** € 600 - € 800  
**Architecturale fit:** Hoog

**Sterke punten:**

- Voldoet volledig aan ADR-020.
- Black-box architectuur.
- Radio-unit kan droog en beschermd worden opgesteld.
- Volledige bediening via CommandMic.
- Consistente gebruikersinterface op alle stations.
- Ondersteuning voor twee CommandMics.
- NMEA 2000 integratie.
- Hailer- en foghornfunctionaliteit.
- Sluit direct aan op bediening vanuit de kuip.

**Aandachtspunten:**

- Hogere aanschafkosten dan een traditionele marifoon.
- Tweede bedieningslocatie vereist een extra CommandMic.
- Meer afhankelijkheid van remote stations.

### Icom IC-M510BB

**Prijsindicatie:** € 900 - € 1.200  
**Architecturale fit:** Hoog

**Sterke punten:**

- Voldoet volledig aan ADR-020.
- Alle voordelen van de IC-M410BB.
- Ondersteuning voor drie CommandMics.
- Voice replay.
- Geïntegreerde AIS-ontvanger.
- Extra integratie- en uitbreidingsmogelijkheden.

**Aandachtspunten:**

- Hogere aanschafkosten.
- AIS-functionaliteit overlapt met het zelfstandige AIS-subsysteem.
- Extra functionaliteit vult momenteel geen expliciete requirement in.

### Standard Horizon GX-1850E + RAM4

**Prijsindicatie:** € 350 - € 500  
**Architecturale fit:** Middel

**Sterke punten:**

- Lagere aanschafkosten.
- NMEA 2000 ondersteuning.
- Ingebouwde GPS.
- Tweede bedieningsstation mogelijk.
- Bewezen en eenvoudige oplossing.

**Aandachtspunten:**

- Hoofdarchitectuur blijft gebaseerd op een hoofdstation binnen.
- Sluit minder goed aan op ADR-020.
- Binnen- en buitenbediening zijn verschillende gebruikersinterfaces.
- Hogere cognitieve belasting.
- Primaire gebruikersinterface blijft gekoppeld aan de hoofdunit.

## Afgevallen selectiecriteria

### AIS-functionaliteit in de marifoon

AIS-functionaliteit wordt geleverd door een afzonderlijk AIS-subsysteem conform ADR-015, ADR-016, ADR-017 en ADR-018.

Geïntegreerde AIS-functionaliteit vormt daarom geen zelfstandig selectiecriterium.

### Dual Watch

Voor de operationele scenario's van Falkor is geen concrete use case geïdentificeerd waarin Dual Watch een expliciete requirement invult.

De aanwezigheid van Dual Watch vormt daarom geen zelfstandig selectiecriterium.

### Voice replay

Voice replay biedt aanvullende functionaliteit, maar vult momenteel geen expliciete requirement in.

Voice replay vormt daarom geen zelfstandig selectiecriterium.

### Derde bedieningsstation

Er bestaat momenteel geen expliciete requirement voor meer dan twee potentiële bedieningslocaties.

Ondersteuning voor een derde bedieningsstation vormt daarom geen zelfstandig selectiecriterium.

## Beoordeling van bedieningslocaties

### Configuratie A

- Eén CommandMic in de kuip.

**Voordelen:**

- Eenvoudig.
- Lage kosten.
- Sluit direct aan op ADR-020.

**Nadelen:**

- Geen fallback-bediening aan kaartentafel.

### Configuratie B

- CommandMic in de kuip.
- CommandMic bij de kaartentafel.

**Voordelen:**

- Primaire bediening in de kuip.
- Fallback-bediening aan kaartentafel.
- Identieke gebruikersinterfaces.
- Intercomfunctionaliteit.

**Nadelen:**

- Hogere kosten.
- Extra hardware.

**Beoordeling:**
Deze configuratie wordt beschouwd als een mogelijke toekomstige uitbreiding van de voorkeursconfiguratie indien operationele ervaring aantoont dat fallback-bediening bij de kaartentafel voldoende meerwaarde biedt.

### Configuratie C

- Twee aansluitpunten.
- Eén verplaatsbare CommandMic.

Voordelen:

- Eén gebruikersinterface.
- Minder hardware.
- Lagere kosten dan twee CommandMics.
- Handset kan eenvoudig worden opgeborgen wanneer Falkor onbeheerd achterblijft.
- Ondersteunt bediening vanuit zowel kuip als kaartentafel.

Nadelen:

- Connectorslijtage door regelmatig verplaatsen.
- Afhankelijkheid van één fysiek apparaat.
- Geen gelijktijdige bediening op meerdere locaties.
- Geen intercomfunctionaliteit tussen locaties.
- Niet geschikt voor operationeel gebruik tijdens passages waarbij regelmatig tussen kuip en kaartentafel wordt gewisseld.

## Huidige voorkeurskeuze

### 1. Icom IC-M410BB

**Beoordeling:** Voorkeursoplossing

De IC-M410BB sluit het beste aan op ADR-020 doordat de architectuur primair uitgaat van een black-box benadering met bediening vanaf de operationele werkplek.

De functionaliteit sluit aan op alle vastgestelde requirements zonder significante overlap met bestaande subsystemen.

### 2. Icom IC-M510BB

**Beoordeling:** Architecturaal gelijkwaardig, functioneel overgedimensioneerd

De IC-M510BB voldoet eveneens uitstekend aan ADR-020.

De meerprijs wordt momenteel niet gerechtvaardigd door expliciete requirements.

### 3. Standard Horizon GX-1850E + RAM4

**Beoordeling:** Functioneel geschikt, architecturaal minder passend

De GX-1850E voldoet functioneel aan vrijwel alle operationele behoeften.

De architectuur sluit echter minder goed aan op ADR-020 doordat deze blijft uitgaan van een hoofdstation binnen met uitbreiding naar buiten.

## Open punten

- Valideren of een tweede CommandMic voldoende meerwaarde biedt ten opzichte van uitsluitend bediening vanuit de kuip.
- Valideren of een aparte externe luidspreker in de kuip daadwerkelijk noodzakelijk is.

## Herbeoordeling

Deze keuze dient opnieuw beoordeeld te worden:

- bij significante prijswijzigingen;
- bij introductie van nieuwe producten;
- bij wijziging van ADR-020;
- bij wijziging van het operationele profiel;
- voorafgaand aan daadwerkelijke aanschaf.
