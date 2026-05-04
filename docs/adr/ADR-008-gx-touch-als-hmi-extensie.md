# ADR-008 — GX Touch display: apart modelleren als HMI-extensie van Cerbo GX

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

Het GX Touch display (GX-display) is los vervangbaar en kan eigen failure modes hebben
(display, kabel, connector) zonder dat de Cerbo GX defect is.
Tegelijkertijd is het display geen systeemdeelnemer (geen N2K/VE_CAN) en HDMI/USB
is geen systeeminterface die op 00 thuishoort.

De vraag is hoe het GX-display wordt gemodelleerd zodat:

- het apart zichtbaar is (replacement/failure modes),
- zonder 00 te vervuilen met HDMI/USB verbindingen,
- en zonder het als generiek display onder 40 te plaatsen.

---

## Beslissingscriteria

- Geen extra systeeminterfaces op 00 voor HDMI/USB.
- Display wél traceerbaar als los onderdeel (BOM/onderhoud).
- Past bij “single source of truth”: geen duplicatie of verkeerde domeinplaatsing.
- Semantisch: display is een HMI-extensie van Cerbo, geen zelfstandig systeemdisplay.

---

## Overwogen opties

### Optie A — Display onder 40 met HDMI sheet-pins naar 00

GX-display als systeem-display met expliciete HDMI/USB koppeling op 00.

### Optie B — Display als apart component bij Cerbo GX (gekozen)

GX-display apart gemodelleerd, lokaal gekoppeld aan Cerbo op het Cerbo-deviceblad.

### Optie C — Display niet modelleren

Alleen als notitie bij Cerbo GX.

---

## Besluit

**Gekozen optie: Optie B — GX-display apart, maar uitsluitend als Cerbo-extensie.**

- Het GX-display wordt als **apart component** gemodelleerd.
- Het wordt uitsluitend gepositioneerd als **HMI-extensie** van de Cerbo GX
  op het Cerbo-deviceblad (lokaal gekoppeld via HDMI/USB).
- Er worden geen sheet-pins of netten toegevoegd aan 00 voor HDMI/USB.
- Het GX-display wordt niet opgenomen als generiek display onder 40.

---

## Gevolgen

### Positief

- Display is zichtbaar als los vervangbaar onderdeel.
- Faalmodi (display/kabel/connector) zijn expliciet zonder Cerbo te belasten.
- 00 blijft schoon en toont alleen systeemrelaties.

### Negatief

- Minder intuïtief voor wie “alle displays onder 40” verwacht; vereist korte toelichting.
- Indien het display ooit eigen voeding/IO krijgt, moet deze ADR worden herzien.

---

## Toepassing en bevestiging

- GX-display verschijnt alleen op het Cerbo-deviceblad als “extension”.
- Geen `HDMI_GX` of vergelijkbare netten op 00.
- Notitie bij de koppeling: mogelijke failure modes en vervangbaarheid.

---

## Notities / vervolg

- Indien later een alternatieve HMI (tablet, remote console) wordt gebruikt, kan dit
  als aparte ADR worden vastgelegd zonder de Cerbo-modellering te wijzigen.
