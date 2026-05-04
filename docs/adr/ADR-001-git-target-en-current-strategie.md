# ADR-001 — Git-strategie voor target (main) en current (as-is) in KiCad

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

Het elektrische systeem van Falkor wordt in meerdere plateaus omgebouwd.
Er is behoefte aan:

1. een **leidende target-architectuur** die ontwerpintentie en eindbeeld beschrijft;
2. **betrouwbare current (as-is) referenties** voor troubleshooting en terugkijken.

De centrale vraag is hoe dit in **Git en KiCad** georganiseerd wordt zonder:

- dubbele waarheid,
- drift tussen schema’s,
- of vervuiling van het target-ontwerp met tijdelijke realiteit.

---

## Beslissingscriteria

- De target-architectuur moet **schoon en intentiegedreven** blijven.
- De current/as-is situatie moet **reproduceerbaar** zijn voor troubleshooting.
- Er mag **geen duplicatie** ontstaan van KiCad-projecten.
- De aanpak moet **werkbaar zijn voor een solo-project** met gefaseerde uitvoering.

---

## Overwogen opties

### Optie A — Twee KiCad-projecten (current en target) in één repository

Twee aparte `.kicad_pro` projecten, elk met eigen schema’s.

### Optie B — Eén KiCad-project; main = target; current snapshots als branches

Eén KiCad-project; de `main` branch beschrijft de target-architectuur.
As-is situaties worden vastgelegd als tijdgebonden branches `current/as-is-YYYY-MM`.

### Optie C — Eén KiCad-project; current en target gemengd met labels

Target en current in dezelfde schema’s, gemarkeerd met labels zoals
`NOT INSTALLED`, `CURRENT ONLY`, etc.

---

## Besluit

**Gekozen optie: Optie B**
Er wordt gewerkt met **één KiCad-project** waarbij:

- de `main` branch de **target-architectuur** beschrijft (bedoelde eindsituatie);
- de huidige installatie wordt vastgelegd in **snapshot-branches**:
  `current/as-is-YYYY-MM`;
- **work/feature branches** worden gebruikt voor experimenten en ontwerpwerk;
- current snapshots **nooit** naar `main` worden gemerged.

Deze aanpak scheidt expliciet **intentie (target)** van **werkelijkheid (current)**,
zonder duplicatie van schema’s of projecten.

---

## Gevolgen

### Positief

- Target blijft een heldere en consistente bron van ontwerpintentie.
- As-is situaties zijn reproduceerbaar voor troubleshooting.
- Verschillen tussen current en target zijn altijd zichtbaar via Git-diff.
- Geen schema-drift door parallelle projecten.

### Negatief

- Discipline vereist: snapshots alleen maken bij betekenisvolle plateau-momenten.
- Het bijwerken van een current snapshot vraagt bewuste verificatie
  van de werkelijke installatie.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast en bewaakt:

- De `main` branch bevat **geen current-only labels** zoals
  `NOT INSTALLED` of `AS-IS`, tenzij het expliciet een **ontwerp-onvolledigheid**
  betreft (`TODO`, `OPTIONAL`, `FUTURE`).
- Elke relevante as-is toestand voor troubleshooting heeft een
  **eigen snapshot-branch** `current/as-is-YYYY-MM`.
- Snapshot-branches worden **niet gemerged** naar `main`.
- Ontwerp- en experimenteerwerk gebeurt uitsluitend in `feature/*` of `work/*`
  branches en wordt alleen naar `main` gemerged als het onderdeel is
  van de target-architectuur.
- In commit messages en ADR’s wordt expliciet gerefereerd aan
  “target” versus “current” context.

---

## Notities / vervolg

- Current snapshots mogen **meestal** starten vanaf de vorige snapshot
  (`current/as-is-(v-1)`) om efficiënt wijzigingen vast te leggen.
- Bij **grote herstructurering** van het target (bijv. hernummering,
  nieuwe facades) of bij **plateau-overgangen** wordt een snapshot
  gestart vanaf `main` om alignment met de target-structuur te waarborgen.
- Deze ADR wordt herzien als meerdere, parallelle eindarchitecturen
  relevant worden (by design scenario’s).
