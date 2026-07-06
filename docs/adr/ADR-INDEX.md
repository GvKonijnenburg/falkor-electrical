# ADR Index — Falkor Electrical

Deze index ordent de Architecture Decision Records (ADR’s) op abstractieniveau en leesvolgorde, niet op historische volgorde.

De nummers zijn stabiel en verwijzen naar concrete besluiten. Nieuwe ADR’s worden altijd toegevoegd met een nieuw, oplopend nummer.

---

## Fundament & werkwijze

*Legt vast hoe het project wordt opgezet, onderhouden en geïnterpreteerd.*

- ADR‑001 — Git‑strategie: target (main) vs current (as‑is)  
- ADR‑002 — Architecturale nummering van KiCad subsheets en facades  
- ADR‑003 — 60‑laag als System Infrastructure

## Operationeel profiel

*Legt vast voor welk gebruiksprofiel de target-architectuur wordt ontworpen.*

- ADR‑019 — Operationeel profiel van Falkor

---

## Platformkeuzes

*Legt vast welke technologie‑ en platformkeuzes in de echte wereld worden gehanteerd en richtinggevend zijn voor de verdere modellering.*

- ADR‑012 — Platformkeuze voor energie
- ADR‑014 — Platformkeuze voor data

---

## Functionele architectuur

*Legt vast hoe systeemcapaciteiten worden gerealiseerd, onafhankelijk van concrete producten.*

- ADR-015 — AIS transmissietechnologie
- ADR-016 — Eisen aan presentatie van AIS-informatie
- ADR-017 — Acceptabele degradatie van AIS-capabilities
- ADR-018 — Antennearchitectuur voor VHF en AIS

---

## Modellering & schema‑grammatica

*Legt vast hoe het systeem, gegeven de platformkeuzes, in KiCad wordt gemodelleerd.*

- ADR‑004 — Domeinindeling: 50_Sensors vs 24_DC_Distribution  
- ADR‑005 — Gebruik van bussen voor fysieke mantels
- ADR-010 — Gebruik van pin-types in KiCad
- ADR-011 — Stekkerverbindingen die normaal gesloten zijn

---

## Netwerkmodellering

*Beschrijft hoe gedeelde netwerken en bussen binnen KiCad worden gerepresenteerd.*

- ADR‑006 — NMEA2000 modelleren als één logisch netwerk  
- ADR‑007 — VE_CAN als ownerless infrastructuurnetwerk + Cerbo GX bridge

---

## Apparaten & concrete keuzes

*Legt vast hoe specifieke componenten binnen de vastgestelde architectuur worden gemodelleerd.*

- ADR‑008 — GX Touch display modelleren als HMI‑extensie van Cerbo GX
