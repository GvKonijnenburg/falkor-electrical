# ADR-010 — Gebruik van pin-types in KiCad voor energieketens (ERC-compatibel)

**Status:** Geaccepteerd  
**Datum:** 2026-05-05

---

## Context en probleemstelling

In KiCad worden pin-types gebruikt om Electrical Rules Check (ERC) mogelijk te maken. Voor energieketens (bijv. DC-voeding van accu naar verbruiker) is het wenselijk dat:

- energiebronnen expliciet als zodanig worden gemodelleerd;
- verbruikers expliciet een voedingsinput hebben;
- ERC kan detecteren wanneer een verbruiker géén voeding ontvangt.

Wanneer tussen bron en verbruiker een schakelend element wordt geplaatst (schakelaar, relais, schakelautomaat), ontstaat een probleem: standaard KiCad-symbolen voor schakelaars hebben uitsluitend **passieve pinnen**, waardoor ERC signaleert dat de verbruiker niet wordt gevoed. De vraag is hoe pin-types zó worden ingezet dat:

- de energierichting semantisch correct blijft;
- ERC bruikbaar en streng blijft;
- het schema intentie blijft uitdrukken, niet wordt “gemanipuleerd” om ERC stil
  te krijgen.

---

## Beslissingscriteria

- Energiebronnen, -doorvoer en -verbruik moeten **expliciet zichtbaar** blijven.
- ERC moet echte fouten kunnen blijven detecteren.
- Modellering moet aansluiten bij de **architecturale intentie** (niet alleen fysisch gedrag).
- Oplossing moet consistent toepasbaar zijn voor alle DC- en AC-energieketens.
- Bekende nadelen moeten expliciet worden afgewogen en gedocumenteerd.

---

## Overwogen opties

### Optie A — Alle pinnen passief maken

Accu’s, schakelaars en verbruikers krijgen passieve pinnen zodat ERC geen fouten meer meldt.

### Optie B — Schakelende elementen modelleren als conditionele doorvoer (gekozen)

Accu’s krijgen `Power Output` pinnen, verbruikers krijgen `Power Input` pinnen. Schakelaars, relais en schakelautomaten krijgen één `Power Input` en één `Power Output` pin, zodat energie logisch “doorloopt” in het schema.

---

## Besluit

**Gekozen optie: Optie B — conditionele doorvoer modelleren.**

In energieketens worden componenten als volgt gemodelleerd:

- **Energiebronnen** (bijv. accu’s, voedingen):
  - pin-type: `Power Output`
- **Verbruikers** (bijv. lamp, koelkast, elektronica):
  - pin-type: `Power Input`
- **Schakelende elementen in de energieketen** (schakelaars, relais,  schakelautomaten):
  - bronzijde: `Power Input`
  - lastzijde: `Power Output`

Hoewel een schakelaar fysiek symmetrisch is, wordt hij in het schema bewust gemodelleerd als **conditionele energiedoorvoer**.

Pin-types worden hiermee gebruikt als **abstract modelleerhulpmiddel** om schema‑intentie en energierichting expliciet te maken en ERC zinvol te laten controleren.

Het generiek passief maken van pinnen om ERC‑waarschuwingen te vermijden wordt expliciet afgewezen.

---

## Gevolgen

### Positief

- Energierichting blijft zichtbaar en eenduidig.
- ERC blijft bruikbaar voor detectie van ontbrekende voedingen.
- Schema’s drukken ontwerpintentie uit in plaats van alleen verbindingstopologie.
- Consistente modellering van switches, relais en beveiliging in energieketens.

### Negatief

- Standaard KiCad-symbolen zijn hiervoor vaak **niet geschikt**.
- Dit vereist het gebruik van **project-specifieke symbolen** met aangepaste pin-types.
- Onderhoud van een **project library** is noodzakelijk.
- Uitwisseling van schema’s met derden vereist extra toelichting.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast:

- Voor energieketens worden uitsluitend symbolen gebruikt waarvan de pin-types overeenkomen met bovenstaande regels.
- Indien nodig worden standaardsymbolen **gekopieerd en aangepast** in een  project-specifieke symbol library.
- De project library wordt onderdeel van de repository en version-controlled.
- ERC-waarschuwingen over ontbrekende voeding worden beschouwd als **echte fouten**  die moeten worden opgelost, niet onderdrukt.
- Voor signaalcontacten en meetpunten (geen energieketen) blijven passieve pinnen toegestaan.

---

## Notities / vervolg

- Het gebruik van een project library wordt **bewust geaccepteerd** als nadeel
  in ruil voor:
  - betere semantiek,
  - betrouwbare ERC,
  - en toekomstvaste schema’s.
- Indien KiCad in toekomstige versies fijnmazigere pin-semantieken introduceert kan deze ADR worden heroverwogen.
- Deze ADR geldt primair voor **energievoorziening**; signaal-routing valt buiten scope.
