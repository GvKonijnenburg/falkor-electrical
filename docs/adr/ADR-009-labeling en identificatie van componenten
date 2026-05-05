# ADR-009 — Labeling en identificatie van componenten

**Status:** Geaccepteerd  
**Datum:** 2026-05-05

---

## Context en probleemstelling

In het elektrische systeem van Falkor is behoefte aan een consistente manier om
**componenten ondubbelzinnig te identificeren** over:

- schema’s (KiCad),
- documentatie (ADR’s, BOM’s),
- fysieke installatie en onderhoud,
- troubleshooting, nu en in de toekomst.

Belangrijk is dat deze identificatie:

- stabiel blijft bij refactors van schema’s,
- niet afhankelijk is van schema‑indeling of bladstructuur,
- en aansluit bij een bestaande, bewezen norm.

De vraag is hoe component‑labeling wordt ingericht zonder:

- semantiek te vermengen met lay‑out,
- dubbele betekenis in labels op te nemen,
- of toekomstige wijzigingen onnodig duur te maken.

---

## Beslissingscriteria

- Labels moeten **object‑identiteit** beschrijven, niet functie of locatie.
- Een componentlabel moet **stabiel blijven** over de levenscyclus.
- Schema‑structuur (bladen, facades) mag **geen invloed** hebben op het label.
- Aansluiting bij een bestaande norm heeft voorkeur boven zelf verzinnen.
- De aanpak moet werkbaar blijven voor een **privé‑project**.

---

## Overwogen opties

### Optie A — Vrije naamgeving per component

Ad‑hoc labels zoals `MP1`, `AIS`, `GPS_nav`.

### Optie B — ISO/IEC 81346‑achtig: typeletter + globaal volgnummer (gekozen)

Componenten krijgen een typeletter (bijv. `J`, `F`, `Q`) gevolgd door een
globaal, oplopend nummer per type.

### Optie C — Typeletter + volgnummer per blad of domein

Bijv. `J24-1`, `J50-2`, gekoppeld aan schema‑structuur.

---

## Besluit

**Gekozen optie: Optie B — ISO/IEC 81346‑achtige component‑identificatie.**

Componenten worden gelabeld volgens een **lightweight toepassing van
ISO/IEC 81346**, gebaseerd op het **product‑aspect** (fysiek object):

```text
<typeletter><volgnummer></volgnummer></typeletter>
```

Voorbeelden:

- `J17` — connector
- `F3` — zekering
- `Q2` — schakelaar / relais
- `A1` — actieve unit (bijv. Cerbo GX)

De betekenis van het label is:
> *“Dit is een uniek fysiek object van dit type in dit systeem.”*

De volgnummering:

- is **globaal per type** (niet per blad of domein);
- zegt **niets** over functie, locatie of schema‑positie;
- verandert **niet** bij herstructurering van schema’s.

---

## Nadere duiding (belangrijk)

- Component‑labels beschrijven **identiteit**, geen gedrag.
- Schema‑positie, bladnummer of domein zijn **documentatie‑context** en geen
onderdeel van het label.
- Het koppelen van identiteit aan schema‑structuur (zoals `J24-1`) wordt
expliciet vermeden, omdat dit labels instabiel maakt bij refactors.

De gekozen aanpak volgt het **principe** van ISO/IEC 81346:

- stabiele object‑identiteit,
- scheiding van aspecten (identiteit ≠ functie ≠ locatie),
zonder de volledige normatieve complexiteit te introduceren.

---

## Gevolgen

### Positief

- Labels blijven stabiel bij wijzigingen in schema‑indeling.
- Schema’s, documentatie en fysieke installatie verwijzen naar hetzelfde object.
- Refactors van target‑architectuur vereisen geen herlabeling.
- Aansluiting bij een breed gebruikte industriële norm.

### Negatief

- Het label zelf geeft geen directe informatie over functie of locatie.
- Navigatie gebeurt via schema en tooling, niet via het nummer.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast:

- Elk fysiek, los vervangbaar object krijgt **één primair component‑label**.
- Het label wordt gebruikt in:
  - schema‑symbolen,
  - documentatie,
  - onderhouds‑ en troubleshooting‑context.
- Labels worden **niet hergebruikt**, ook niet na verwijdering van componenten.
- Aanvullende context (rol, fysiek gebied) mag worden vastgelegd in
  documentatievelden, maar maakt **geen onderdeel van het label** uit.
- Verbindings‑ en netlabels (bijv. `VE_CAN`, `N2K`, `DC_POS_HOUSE`) vallen
  expliciet **niet** onder deze ADR.

---

## Notities / vervolg

### Verwachte componenttypen en bijbehorende typeletters

Onderstaande lijst beschrijft de **verwachte componenten aan boord van Falkor**
en de bijbehorende typeletter. Deze lijst is richtinggevend en kan worden
uitgebreid via nieuwe ADR’s indien nodig.

- `A` — Actieve systemen / units  
  (bijv. Cerbo GX, MultiPlus II, AIS transponder, plotter)

- `B` — Batterijen / accublokken  
  (bijv. house battery bank, startaccu)

- `F` — Zekeringen en smeltzekeringen  
  (fuse holders, inline fuses)

- `H` — Bedienings- en indicatie‑elementen  
  (knoppen, leds, buzzers, eenvoudige HMI‑elementen)

- `J` — Connectoren en aansluitpunten  
  (stekkers, doorvoeren, klemmen die als object worden beschouwd)

- `Q` — Schakelaars, relais, contactoren  
  (mechanisch of elektrisch aangestuurd, inclusief schakelautomaten)

- `X` — Klemmenblokken / terminals  
  (vaste aansluitklemmen, terminal strips)

- `Y` — Antennes en RF‑componenten
  (RF antenne)

- `S` — Sensoren  
  (wind, diepte, log, GPS ontvangers, tankgevers)

Deze lijst is **niet uitputtend** en beschrijft het initiële
lettergebruik voor dit project. Aanvulling of verfijning gebeurt
uitsluitend via een nieuwe ADR.

---

#### A — Actieve systemen / units

De typeletter **A** wordt gebruikt voor **zelfstandige, actieve apparaten** die:

- eigen interne logica, regeling of software bevatten;
- autonoom gedrag vertonen (meer dan passieve doorvoer of indicatie);
- als **één functionele eenheid** worden vervangen of onderhouden;
- meerdere interne functies combineren (bijv. sensorverwerking, besturing,
  communicatie, vermogensregeling).

Kenmerken van een A‑component:

- het apparaat kan “iets doen” zonder externe logica;
- de interne samenstelling (motoren, voedingen, drivers, firmware) wordt
  **niet afzonderlijk gemodelleerd**;
- faalgedrag en vervanging gebeuren op apparaatniveau, niet op onderdeel­niveau.

Een apparaat krijgt **geen aparte labels voor interne onderdelen**.
Een motor, voeding of regelprint binnen een A‑component wordt gezien
als integraal onderdeel van het apparaat en niet als zelfstandig object.

De typeletter **A** drukt geen energierol uit (verbruiker, bron, opslag),
maar uitsluitend het feit dat het gaat om een **actief systeem met eigen gedrag**.
