# ADR-003 — 60-laag als System Infrastructure (Physical & Protocol)

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

In het elektrische schema van Falkor moeten zowel:

- **functionele systeemrelaties** (wie levert energie of data aan wie),
- als **fysieke en protocolmatige implementatie** (bekabeling, topologie, terminators)

worden vastgelegd.

Het risico is dat deze twee perspectieven:

- door elkaar gaan lopen,
- of dat het top-level schema (00) vervuilt met implementatiedetails.

De vraag is hoe fysieke/protocolmatige details expliciet gedocumenteerd kunnen
worden zonder de functionele architectuur aan te tasten.

---

## Beslissingscriteria

- Functionele architectuur moet **begrijpelijk blijven zonder detailkennis**.
- Het top-level (00) moet **systeemrelaties tonen, geen kabeltopologie**.
- Fysieke implementatie moet **wel** traceerbaar zijn voor installatie en onderhoud.
- Apparaten mogen **niet gedupliceerd** worden over meerdere lagen.
- De oplossing moet schaalbaar zijn bij groei van het systeem.

---

## Overwogen opties

### Optie A — Volledige topologie tekenen op 00

Alle kabels, T‑stukken, terminators en looms zichtbaar maken op het top‑level schema.

### Optie B — Afzonderlijke infrastructuurlaag (gekozen)

Een aparte architectuurlaag waarin fysieke en protocolmatige implementatie
wordt uitgewerkt, los van functionele facades.

### Optie C — Geen fysieke topologie modelleren

Alleen logische netlabels gebruiken; fysieke uitleg volledig buiten KiCad laten.

---

## Besluit

**Gekozen optie: Optie B — Afzonderlijke infrastructuurlaag (60)**
Er wordt een expliciete **60-laag** geïntroduceerd met de naam:

> `60_System_Infrastructure_(Physical_&_Protocol)`

Deze laag heeft een **verklarende functie** en bevat:

- fysieke topologie (bekabeling, looms);
- protocol-specifieke structuren (bijv. N2K backbone + T‑stukken, VE.Can daisy‑chain);
- terminatie, connector‑ en tap‑punten.

De 60‑laag **voegt geen nieuwe functionaliteit toe** en draagt geen systeemintentie.
Zonder de 60‑laag blijft het systeem functioneel correct en begrijpelijk.

---

## Gevolgen

### Positief

- Het top‑level schema (00) blijft een zuivere systeemkaart.
- Functionele facades worden niet vervuild met kabel- of protocoldetails.
- Fysieke installatie is toch expliciet en onderhoudbaar gedocumenteerd.
- Troubleshooting van netwerken krijgt een duidelijke, vaste plek.

### Negatief

- Extra discipline vereist om implementatiedetails niet alsnog in facades te tekenen.
- Fysieke topologie moet actief bijgehouden worden bij installatiewijzigingen.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast en bewaakt:

- In `00_TopLevel` worden uitsluitend:
  - functionele relaties,
  - logische netten,
  - en systeemrollen getoond.
- De 60‑laag bevat uitsluitend infrastructuur-uitleg.
- Apparaten worden **niet** opnieuw getekend in 60;
  alleen taps/connectorpunten met verwijzing naar device‑ID’s zijn toegestaan.
- Detailbladen onder 60 worden genummerd (61, 62, 63, …) als **inhoudelijke index**,
  niet als subdomeinen.

---

## Notities / vervolg

- De 60‑laag is expliciet **niet hiërarchisch gelijkwaardig** aan facades zoals
  AC (10), DC (20), Sensors (50).
- Indien nieuwe infrastructuurtypen ontstaan (bijv. Ethernet/SignalK),
  worden deze onder 60 toegevoegd en niet als nieuwe facades gemodelleerd.
  