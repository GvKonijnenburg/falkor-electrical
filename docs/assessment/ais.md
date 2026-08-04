# AIS Transponder Assessment

**Status:** Huidige voorkeurskeuze4
**Datum:** 2026-07-06

## Context

Deze beoordeling vertaalt de huidige architectuur naar een concrete productvoorkeur. Het document heeft geen normatief karakter en legt geen architectuurbesluiten vast. De beschreven voorkeur geldt uitsluitend op basis van het huidige marktaanbod en de huidige prijzen.

## Architecturale uitgangspunten

- ADR-014 — Platformkeuze voor data
- ADR-015 — AIS-transmissietechnologie
- ADR-016 — Eisen aan presentatie van AIS-informatie
- ADR-017 — Acceptabele degradatie van AIS-capabilities
- ADR-018 — Antennearchitectuur voor VHF en AIS

## Geïntegreerde versus externe splitter

ADR-018 geeft de voorkeur aan een zelfstandige splitter als infrastructuurcomponent.

Tijdens de evaluatie is vastgesteld dat geïntegreerde splitters praktische voordelen kunnen bieden, waaronder:

- minder componenten;
- minder bekabeling;
- eenvoudigere installatie.

Deze voordelen zijn onvoldoende om ADR-018 te herzien, maar zijn wel legitieme argumenten bij de beoordeling van concrete producten. Producten met geïntegreerde splitters worden daarom niet uitgesloten, maar beoordeeld op hun totale architecturale en praktische fit.

## Kandidaatoplossingen

### em-trak B951

**Prijsindicatie:** € 650

**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Externe splitterarchitectuur
- Geen functies waarvoor momenteel geen requirement bestaat

### em-trak B952

**Prijsindicatie:** € 900

**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Externe splitterarchitectuur
- WiFi
- Bluetooth


**Aandachtspunten:**

- Hogere kosten dan de B951
- Vereist een afzonderlijke splitter conform ADR-018
- Extra functionaliteit vult momenteel geen expliciete requirement in

### em-trak B953

**Prijsindicatie:** € 850
**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Geïntegreerde splitter
- Minder afzonderlijke componenten
- Eenvoudigere fysieke installatie

**Aandachtspunten:**

- Hogere kosten dan de B951
- Geïntegreerde splitter wijkt af van de voorkeursarchitectuur uit ADR-018
- Vervanging van de AIS-transponder beïnvloedt tevens de splitterfunctie
- Minder onafhankelijke vervangbaarheid van subsystemen

### Raymarine AIS700

**Prijsindicatie:** € 1.000
**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Sterke integratie met Raymarine-ecosysteem
- Geïntegreerde splitter
- Minder afzonderlijke componenten
- Eenvoudigere fysieke installatie

**Aandachtspunten:**

- Hogere kosten dan de B951
- Geïntegreerde splitter wijkt af van de voorkeursarchitectuur uit ADR-018
- Vervanging van de AIS-transponder beïnvloedt tevens de splitterfunctie
- Minder onafhankelijke vervangbaarheid van subsystemen

## Huidige voorkeurskeuze

1. B951
   Beste match met huidige requirements.
1. B953
   Eenvoudigere installatie tegen een verdedigbare meerprijs.
1. B952
   Extra functionaliteit zonder expliciete requirement.
1. AIS700
   Functioneel geschikt maar minder aantrekkelijk geprijsd.

Deze keuze dient opnieuw beoordeeld te worden:

- bij significante prijswijzigingen;
- bij introductie van nieuwe producten;
- bij wijziging van de architectuur;
- voorafgaand aan daadwerkelijke aanschaf.
