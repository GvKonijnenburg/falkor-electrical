# ADR-005 — Gebruik van fysieke bussen voor mantels (AC_IN, mast-looms) en KiCad bus-notatie

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

In het schema komen meerdere situaties voor waarin **één fysieke mantel/loom** meerdere aders bevat
(bijv. walstroomkabel met L/N/PE, mastbekabeling voor toplichten en deklicht).
Zonder bundeling wordt het top-level (00) snel visueel druk en wordt fysieke realiteit ("één kabel")
niet goed zichtbaar.

KiCad ondersteunt bussen op meerdere manieren (platte bus vs geneste bus). De vraag is:

- wanneer gebruiken we een bus;
- en welke KiCad bus-notatie gebruiken we, zodat semantiek (betekenis van aders) zuiver blijft.

---

## Beslissingscriteria

- Een bus moet een **fysiek kabelobject** representeren (mantel/loom), niet alleen cosmetische bundeling.
- Fundamentele nets (zoals AC_L/AC_N/PE) moeten hun **zelfstandige betekenis** behouden.
- De oplossing moet leesbaarheid verbeteren op 00 zonder extra “magie” of nieuwe netwerken te suggereren.
- Consistent met mast-looms en andere fysieke bundels.

---

## Overwogen opties

### Optie A — Geneste bus-notatie (BUS{...} → BUS.NET)

Aders krijgen gescopede namen zoals `AC_IN.AC_L`.

### Optie B — Platte bus-notatie (BUS = { NET1 NET2 ... }) (gekozen)

Bus bundelt bestaande nets met zelfstandige betekenis: `AC_IN = { AC_L, AC_N, PE }`.

### Optie C — Geen bus; losse aders tekenen

L/N/PE en mast-aders als losse verbindingen tussen bladen.

---

## Besluit

**Gekozen optie: Optie B — Platte bus-notatie voor fysieke mantels.**

- Een bus wordt alleen gebruikt wanneer er fysiek een **mantel/loom** is.
- De bus bundelt bestaande nets; de aders behouden hun eigen netnaam.
- De geneste notatie (`AC_IN.AC_L`) wordt vermeden, omdat die een kunstmatige naamruimte introduceert.

Voorbeeld walstroom:

- Op 00: connector `J_SHORE_AC` met nets `AC_L`, `AC_N`, `PE`.
- Busdefinitie: `AC_IN = { AC_L, AC_N, PE }`.
- Naar `10_Power_AC`: één busverbinding `AC_IN`.

Voorbeeld mast:

- Per mantel/connector een eigen bus, bijvoorbeeld:
  - `MAST_TOP = { MAST_3COL_POS, MAST_ANCHOR_POS, MAST_TOP_NEG }`
  - `MAST_DECK = { MAST_DECK_POS, MAST_DECK_NEG }`

---

## Gevolgen

### Positief

- 00 blijft compact: één mantel = één verbinding.
- Aders behouden semantiek (PE blijft PE; geen `AC_IN.PE`).
- Consistent patroon voor alle fysieke bundels (mast, walstroom, etc.).

### Negatief

- Discipline nodig: bus alleen gebruiken als er echt één mantel is.
- Bij wijziging in loom-samenstelling moet de busdefinitie worden bijgewerkt.

---

## Toepassing en bevestiging

- In reviews geldt: **bus = fysieke mantel/loom**.
- Bus-notatie is altijd “plat” (`BUS = { NET1, NET2 }`).
- Geneste bus-notatie wordt alleen toegestaan na expliciete ADR-wijziging.

---

## Notities / vervolg

- Voor RF coax wordt geen bus gebruikt; coax is één signaalpad met shield (indien gemodelleerd).
- Voor N2K/VE_CAN blijven netlabels leidend; fysieke topologie wordt in 60 beschreven (ADR-003).
