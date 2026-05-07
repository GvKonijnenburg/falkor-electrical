# ADR-011 — Modelleren van stekkerverbindingen die normaal aangesloten zijn

**Status:** Geaccepteerd  
**Datum:** 2026-05-05

---

## Context en probleemstelling

In het elektrische systeem van Falkor komen verbindingen voor die fysiek bestaan uit een stekker/contra‑stekkerpaar, maar die in de normale bedrijfstoestand permanent aangesloten zijn (bijv. apparaten met afneembare voedingskabels).

De vraag is hoe deze verbindingen gemodelleerd worden in KiCad zonder:

- energieketens kunstmatig te onderbreken;
- ERC‑controle onbruikbaar te maken;
- of functionele schema’s te laten afhangen van implementatiedetails.

---

## Beslissingscriteria

- Het schema moet de **normale bedrijfstoestand** van het systeem beschrijven.
- Energieketens moeten functioneel gesloten blijven in ERC‑analyse.
- Fysieke losneembaarheid moet wel **documenteerbaar** blijven.
- Scheiding tussen functionele architectuur en implementatie moet behouden blijven.

---

## Overwogen opties

### Optie A — Stekkerpaar modelleren in functionele schema’s

De stekker en het stopcontact worden expliciet opgenomen tussen bron en verbruiker, waardoor de energiestroom formeel wordt onderbroken.

### Optie B — Stekkerpaar alleen modelleren in infrastructuurlaag (gekozen)

In functionele schema’s wordt de verbinding als permanent gesloten gemodelleerd. De fysieke stekkerverbinding wordt uitsluitend vastgelegd in 60_System_Infrastructure.

---

## Besluit

**Gekozen optie: Optie B — scheiding van functie en implementatie.**

Het functionele schema beschrijft uitsluitend de **normale bedrijfstoestand** van het systeem. Fysiek losneembare verbindingen die in normaal gebruik aangesloten blijven, worden daarin als permanent gesloten gemodelleerd.

Stekker/contra‑stekkerparen, kabels en fysieke loskoppeling worden vastgelegd in de infrastructuurlaag (60), waar implementatiedetails thuishoren.

---

## Gevolgen

### Positief

- Energieketens blijven logisch en gesloten.
- ERC kan betrouwbaar controleren of verbruikers worden gevoed.
- Functionele schema’s blijven leesbaar en intentiegericht.
- Fysieke realiteit blijft volledig documenteerbaar.

### Negatief

- Losneembaarheid is niet zichtbaar in het functionele schema.
- Begrip van fysieke installatie vereist raadpleging van de 60‑laag.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast:

- In functionele bladen (00, 10, 20, 24, 50) worden geen losse stekkerparen  gemodelleerd voor verbindingen die normaal gesloten zijn.
- In `60_System_Infrastructure` worden stekker/contra‑stekkerparen expliciet gemodelleerd met passende componentlabels (bijv. `Jxx`).
- ERC‑waarschuwingen door onderbroken energieketens worden beschouwd als fouten, niet als acceptabele modelleringstoestand.
- Alleen verbindingen die **functioneel bedoeld zijn om regelmatig los te zijn** (bijv. service‑interfaces) mogen als stekkerpaar in functionele schema’s worden getoond.

---

## Notities / vervolg

- Dit besluit sluit aan bij ADR‑003 (scheiding functie vs. implementatie),
  ADR‑008 (infrastructuurdetails in 60) en ADR‑010 (betekenisvolle ERC‑controle).
- Indien een fysieke loskoppeling ook een normale functionele toestand is,
  dient dit expliciet per geval te worden beoordeeld en vastgelegd in een aparte ADR.

  ### Voorbeelden

**Voorbeeld 1 — Aansluitingen bij de mastvoet.**

Sensor- en instrumentbekabeling vanaf de mast (wind, log, navigatieverlichting) loopt doorgaans via één of meerdere losneembare stekkerverbindingen bij de mastvoet.In normaal bedrijf blijft deze verbinding permanent aangesloten; loskoppeling gebeurt uitsluitend voor demontage van de mast.

- In functionele schema’s (bijv. 50_Sensors, 00_TopLevel) worden deze verbindingen als permanent gesloten gemodelleerd.
- De fysieke stekker/contra‑stekkerparen, connectoren en kabelovergangen worden expliciet vastgelegd in `60_System_Infrastructure`, bijvoorbeeld in  `64_Mast_Wiring`, met bijbehorende `Jxx`‑labels.

De losneembaarheid van de mastvoetverbinding is een installatie‑eigenschap,
geen functionele toestand van het systeem.

---

**Voorbeeld 2 — AC‑aansluiting van de boiler.**

Een elektrische boiler is aangesloten via een stekker op een wandcontactdoos of servicestopcontact, terwijl deze stekker in normaal gebruik permanent ingestoken blijft.

- In het functionele AC‑schema wordt de boiler als vast aangesloten verbruiker gemodelleerd, zodat de AC‑energieketen logisch en gesloten blijft.
- De stekkerverbinding zelf wordt alleen vastgelegd in de infrastructuurlaag (`60_System_Infrastructure`), inclusief stekker, contactdoos en kabel.

Alleen wanneer loskoppeling van de boiler een **normale functionele handeling** zou zijn (bijv. frequent wisselen tussen verbruikers), zou modellering als stekkerpaar in het functionele schema overwogen worden.
