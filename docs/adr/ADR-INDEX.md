# ADR Index — Falkor Electrical

Deze index ordent de Architecture Decision Records (ADR’s) op **abstractieniveau en leesvolgorde**, niet op historische volgorde.

De nummers zijn stabiel en verwijzen naar concrete besluiten. Nieuwe ADR’s worden altijd toegevoegd met een nieuw, oplopend nummer.

---

## Fundament & werkwijze

Besluiten die de **werkwijze, waarheid en architecturale kaders** vastleggen. Deze ADR’s vormen het uitgangspunt voor alle andere beslissingen.

- **ADR‑001** — Git‑strategie: target (main) vs current (as‑is)  
- **ADR‑002** — Architecturale nummering van KiCad subsheets en facades  
- **ADR‑003** — 60‑laag als System Infrastructure (Physical & Protocol)

---

## Modellering & schema‑grammatica

Besluiten die beschrijven **hoe** het systeem in KiCad wordt gemodelleerd, los van specifieke technologie of apparaten.

- **ADR‑004** — Domeinindeling: 50_Sensors vs 24_DC_Distribution  
- **ADR‑005** — Gebruik van bussen voor fysieke mantels (AC_IN, mast‑looms)
- **ADR-010** — Gebruik van pin-types in KiCad
- **ADR-011** — Stekkerverbindingen die normaal gesloten zijn

---

## Netwerken & communicatie

Besluiten over **gedeelde netwerken en datadomeinen** en hun samenhang.

- **ADR‑006** — NMEA2000 modelleren als één logisch netwerk  
- **ADR‑007** — VE_CAN als ownerless infrastructuurnetwerk + Cerbo GX bridge

---

## Apparaten & concrete keuzes

Besluiten over **specifieke componenten** en hun modellering binnen de vastgestelde architectuur.

- **ADR-012** — Platformkeuze voor energie
- **ADR‑008** — GX Touch display modelleren als HMI‑extensie van Cerbo GX

---

## Leesadvies

Voor een goed begrip van het systeem en de onderliggende keuzes:

1. Lees eerst alle ADR’s onder **Fundament & werkwijze**  
   (werkwijze, nummering, scheiding tussen functie en infrastructuur).

2. Ga daarna verder met **Modellering & schema‑grammatica**  
   (hoe het systeem in KiCad wordt vastgelegd).

3. Lees vervolgens **Netwerken & communicatie**  
   (datadomeinen en bridges tussen subsystemen).

4. Lees tot slot **Apparaten & concrete keuzes**  
   (specifieke componenten en hun modellering).
