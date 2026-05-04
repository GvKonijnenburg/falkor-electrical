# ADR-002 — Architecturale nummering van KiCad subsheets en facades

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

Bij het opzetten van een nieuw KiCad‑project voor het elektrische systeem van Falkor
is behoefte aan een **consistente en toekomstvaste structuur** voor het top‑down
modelleren van het systeem.

Daarbij moet in één oogopslag duidelijk zijn:

- in welk **systeemdomein** een blad of subsysteem valt;
- hoe dit blad zich **architecturaal** verhoudt tot andere delen van het systeem;
- en hoe hiernaar gerefereerd kan worden in documentatie, ADR’s en commits.

De vraag is hoe subsheets logisch genummerd en benoemd worden op een manier die
schaalbaar is en losstaat van layout of KiCad‑paginanummering.

---

## Beslissingscriteria

- Nummers moeten **semantische betekenis** hebben (domein / rol).
- Nummering moet **stabiel** blijven bij uitbreiding of herstructurering.
- De structuur moet **top‑down denken** ondersteunen.
- Verwijzingen in documentatie en Git moeten eenduidig zijn.
- Nummering mag **niet afhankelijk zijn van KiCad lay‑out of exportvolgorde**.

---

## Overwogen opties

### Optie A — Geen nummering, alleen beschrijvende namen

Bijv. `Power_AC`, `Power_DC`, `Sensors`, `Infrastructure`.

### Optie B — Architecturale nummering per domein (gekozen)

Vaste nummerblokken per hoofd­domein, gebruikt in bestands‑ en sheet‑namen
(bijv. `10_Power_AC`, `20_Power_DC`).

### Optie C — Nummering gebruiken als KiCad paginanummers

Architecturale nummers gelijk laten lopen met KiCad export-/paginanummers.

---

## Besluit

**Gekozen optie: Optie B — Architecturale nummering per domein**
De volgende nummering wordt gehanteerd als **architecturale identificatie**:

- `00` — Top‑level overzicht en systeemrelaties  
- `10` — Power AC  
- `20` — Power DC
  - `24` — DC distributie en endpoints (subdomein van 20)  
- `30` — Engine / voortstuwing (indien relevant)  
- `40` — Displays & bediening  
- `50` — Sensoren (beginpunten van informatie)  

De nummers vormen **onderdeel van de architectuur** en worden gebruikt in:

- sheet‑namen,
- bestandsnamen,
- documentatie,
- ADR’s,
- commit‑messages.

---

## Interpretatie van nummering (belangrijk)

De gehanteerde nummers zijn **architecturale identificatoren** en **geen KiCad
paginanummers**.

Concreet betekent dit:

- De nummers drukken **systeemdomein en architecturale positie** uit.
- Ze zijn **semantisch**, niet layout‑gedreven.
- Ze blijven **stabiel**, ook als:
  - de volgorde van sheets wijzigt,
  - nieuwe bladen worden toegevoegd,
  - of exports anders worden ingedeeld.

KiCad paginanummers en exportvolgorde worden beschouwd als
**presentatiehulpmiddel**, niet als dragers van architecturale betekenis.

---

## Gevolgen

### Positief

- In één oogopslag zichtbaar in welk domein een blad thuishoort.
- Eenduidige referenties in ontwerpdiscussies en documentatie
  (bijv. “dit hoort onder 24, niet bij 50”).
- Schaalbaar bij uitbreiding van het systeem zonder hernummering.
- Onafhankelijk van KiCad layout‑ en exportgedrag.

### Negatief

- Een kort gewenmoment nodig voor het onderscheid tussen
  architectuurnummer en paginanummer.
- Disciplinair: nummers niet misbruiken voor lay‑outvolgorde.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast en bewaakt:

- Elk KiCad sheet en bijbehorend bestand gebruikt het afgesproken
  architectuurnummer in naam en titel.
- In documentatie en ADR’s wordt **altijd** naar het architectuurnummer verwezen,
  nooit naar paginanummers.
- KiCad paginanummers worden niet gebruikt als referentie in tekst of commits.
- Optioneel kan het architectuurnummer zichtbaar worden gemaakt
  in het title‑block (bijv. `ARCH-ID: 24`), zonder impact op paginanummering.

---

## Notities / vervolg

- Subnummers (zoals `24` onder `20`) geven **subdomeinen** aan, geen hiërarchische
  paginavolgorde.
- Indien nieuwe hoofddomeinen ontstaan, worden deze toegevoegd met een nieuw
  tientalnummer en vastgelegd via een nieuwe ADR.

### Gebruik van nummers binnen een hoofddomein

Binnen een hoofddomein kunnen genummerde bladen voorkomen met *verschillende
betekenisniveaus*. Niet elk nummer duidt een subdomein aan.

#### Architecturaal subdomein

Een **subdomein** wordt alleen toegekend wanneer binnen een hoofddomein sprake is
van een **blijvend onderscheiden architecturale verantwoordelijkheid**.

Kenmerken van een subdomein:

- markeert een structurele scheiding van verantwoordelijkheden;
- heeft een eigen wijzigings- en faalcontext;
- is relevant voor ontwerp, onderhoud en troubleshooting;
- wordt expliciet als zodanig benoemd.

Momenteel is deze situatie uitsluitend aanwezig binnen het DC‑domein:

- `20_Power_DC` beschrijft energie-opwekking, opslag en conversie;
- `24_DC_Distribution` beschrijft distributie, beveiliging (CB’s/zekeringen)
  en voeding van endpoints en sensoren.

#### Ordinale bladnummering

Binnen een hoofddomein kunnen daarnaast **genummerde bladen voorkomen die géén
subdomein representeren**. Deze nummers dienen uitsluitend voor:

- inhoudelijke groepering;
- navigatie;
- stabiele referentie in schema’s en documentatie.

Voorbeelden hiervan zijn bladen zoals `23_Laden`.

Deze nummering heeft **geen architecturale zelfstandigheidsbetekenis** en
introduceert geen nieuw domein of subdomein.

### Keuze van subnummer 24

Het subnummer `24` is bewust gekozen en heeft **geen kwantitatieve of
volgordebetekenis**.

De keuze voor `24` volgt deze ontwerpregels:

- `20` blijft de **ankerpositie** voor het DC-hoofddomein.
- Subnummers gebruiken **ruimte binnen het tiental** (21–29), zodat:
  - toekomstige subdomeinen kunnen worden toegevoegd zonder hernummering;
  - het hoofddomein (`20`) visueel dominant blijft.
- `24` ligt:
  - niet direct naast `20` (vermijdt verwarring met detail- of volgnummering);
  - niet aan de rand (`21`/`29`), zodat uitbreiding naar beide kanten mogelijk blijft.

Concreet:

- `21–23` blijven beschikbaar voor eventuele DC-opwekking/conversie-subdomeinen;
- `25–28` blijven beschikbaar voor toekomstige DC-gerelateerde scheidingen;
- `24` fungeert als neutrale, stabiele positie voor distributie en beveiliging.

Het nummer `24` is daarmee een **positionele keuze**, geen technische of
numerieke noodzaak.
