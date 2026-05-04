# ADR-006 — NMEA2000 (N2K) modelleren als één logisch netwerk

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

NMEA2000 (N2K) is een gedeeld netwerk waarop data als berichten (PGNs) circuleert.
Bij modellering in KiCad ontstaat de verleiding om per datatype (GPS, wind, diepte) aparte
"signalen" of nets te maken.

De vraag is hoe we N2K modelleren zodat:

- het protocol-juist blijft (één netwerk),
- bron van data traceerbaar blijft,
- en het schema schaalbaar blijft bij veel sensoren.

---

## Beslissingscriteria

- N2K blijft één logisch netwerk (geen impliciete segmentatie per datatype).
- Apparaten blijven single source of truth (niet dupliceren voor datastromen).
- Herkomst van data blijft begrijpelijk via apparaatnaam/annotatie.
- Topologie (backbone/T-stukken/terminators) blijft in 60 (ADR-003), niet op 00.

---

## Overwogen opties

### Optie A — Per datatype een apart N2K_* net

Bijv. `N2K_GPS`, `N2K_WIND`, `N2K_DEPTH`.

### Optie B — Eén N2K net; bronrol via device-naam/annotatie (gekozen)

Alle apparaten hebben één `N2K` poort op hetzelfde netlabel `N2K`.

### Optie C — Eén N2K net + rol-pinnen op devices

Pinnaam draagt rol (bijv. `N2K_GPS_SRC`) maar wordt elektrisch op hetzelfde net aangesloten.

---

## Besluit

**Gekozen optie: Optie B — Eén N2K netwerk als netlabel `N2K`**

- Op 00 bestaat één logisch net `N2K` waaraan deelnemers worden verbonden.
- Apparaten (sensorgeving onder 50; endpoints onder 24/40) krijgen een `N2K` poort.
- Het is impliciet dat een apparaat dat als GPS-sensor is gemodelleerd GPS-data publiceert.
- Voor multi-role devices (bijv. plotter die GPS data publiceert) wordt de rol
  vastgelegd als annotatie ("publishes GPS on N2K").

Optie C mag als uitzondering wanneer een device meerdere onafhankelijke datarollen heeft
en expliciete rol-pinnen de leesbaarheid aantoonbaar verhogen.

---

## Gevolgen

### Positief

- Protocol-juist: N2K blijft één netwerk.
- Schema blijft schaalbaar bij groei in aantal sensoren.
- Geen schijn van meerdere N2K-netwerken per datatype.

### Negatief

- Zonder annotaties is niet zichtbaar welke PGNs een device publiceert.
- Rol-pinnen kunnen verleidelijk zijn; gebruik ze spaarzaam en consistent.

---

## Toepassing en bevestiging

- Op 00 wordt één netlabel `N2K` gebruikt.
- In detailblad `62_N2K` (onder 60) wordt backbone/topologie beschreven,
  zonder dat dit de logische koppeling op 00 verandert.
- Per-datatype nets (`N2K_GPS`, etc.) worden niet geïntroduceerd.

---

## Notities / vervolg

- Dataflow (wie publiceert wat) wordt primair via apparaatnaam en annotatie geduid.
- Bij complexe situaties kan een aanvullend document of annotatiestandaard
  voor PGNs worden toegevoegd.
