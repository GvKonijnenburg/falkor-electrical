# ADR-XXX — <Korte, beschrijvende titel>

**Status:** voorgesteld | geaccepteerd | vervangen | achterhaald  
**Datum:** YYYY-MM-DD  

---

## Context en probleemstelling

Beschrijf kort de context waarin deze beslissing is genomen en welk probleem
of welke ontwerpvraag moest worden opgelost.

Richtlijn:
- 1–2 alinea’s
- Beschrijf *waarom* deze beslissing nodig was
- Formuleer eventueel expliciet de vraag

Voorbeelden:
- Hoe modelleren we VE_CAN zonder eigenaarschap toe te wijzen?
- Hoe beheren we current vs target architectuur tijdens een gefaseerde refit?

---

## Beslissingscriteria

Welke overwegingen waren bepalend voor deze beslissing?

Gebruik alleen criteria die daadwerkelijk relevant waren.

Voorbeelden:
- Begrijpelijkheid voor future me
- Lange‑termijn onderhoudbaarheid
- Scheiding tussen intentie (target) en werkelijkheid (current)
- Beperkingen van KiCad of Git
- Voorkomen van drift en dubbel modelleren

---

## Overwogen opties

Welke realistische opties zijn onderzocht?

### Optie A — <titel>
Korte beschrijving van deze optie.

### Optie B — <titel>
Korte beschrijving van deze optie.

### (optioneel) Optie C — <titel>
Alleen opnemen als deze echt serieus overwogen is.

---

## Besluit

**Gekozen optie:** <titel>

**Motivatie:**

Leg uit:
- waarom deze optie is gekozen
- waarom de andere opties zijn afgevallen

Focus op *argumenten*, niet op herhaling van criteria.

---

## Gevolgen

### Positief
- …
- …

### Negatief / trade-offs
- …
- …

Elke beslissing heeft nadelen; benoem ze expliciet.

---

## Toepassing en bevestiging

Hoe wordt deze beslissing geborgd in de praktijk?

Voorbeelden:
- Schema’s volgen consequent dit patroon
- Afwijkingen vereisen een expliciete nieuwe ADR
- Bij twijfel: deze ADR herlezen vóór aanpassen van de architectuur

Dit hoeft niet geautomatiseerd te zijn; bewustzijn is voldoende.

---

## Notities en vervolg

(optioneel)

Gebruik dit voor:
- relatie met andere ADR’s
- wanneer deze beslissing herzien moet worden
- zaken die bewust *niet* door deze ADR zijn opgelost