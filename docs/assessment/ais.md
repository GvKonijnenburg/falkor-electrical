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

## Kandidaatoplossingen

### em-trak B951

**Prijsindicatie:** € 650

**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Externe splitterarchitectuur
- Geen functies waarvoor momenteel geen requirement bestaat

**Aandachtspunten:**

- Geen WiFi/Bluetooth

### em-trak B952

**Prijsindicatie:** € 850

**Architecturale fit:** Hoog

**Sterke punten:**

- Voldoet aan alle eisen van de B951
- WiFi
- Bluetooth
- Extra distributiemogelijkheden

**Aandachtspunten:**

- Hogere kosten
- Extra functionaliteit vult momenteel geen expliciete requirement in

### Raymarine AIS700

**Prijsindicatie:** € 995

**Architecturale fit:** Hoog

**Sterke punten:**

- SOTDMA
- NMEA 2000
- Sterke integratie met Raymarine-ecosysteem
- Ingebouwde splitter

**Aandachtspunten:**

- Hogere kosten
- Geïntegreerde splitter past minder goed bij ADR-018
- Sterkere koppeling tussen transponder en antenne-infrastructuur
- Minder onafhankelijke vervangbaarheid van subsystemen

## Huidige voorkeurskeuze

1. em-trak B951
1. em-trak B952
1. Raymarine AIS700

Deze keuze dient opnieuw beoordeeld te worden:

- bij significante prijswijzigingen;
- bij introductie van nieuwe producten;
- bij wijziging van de architectuur;
- voorafgaand aan daadwerkelijke aanschaf.
