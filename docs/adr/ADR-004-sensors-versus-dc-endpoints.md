# ADR-004 — Scheiding tussen sensoren (50) en DC-endpoints & distributie (24)

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

In het elektrische schema van Falkor komen veel apparaten voor die:

- elektrische energie verbruiken (DC),
- én data genereren of doorgeven.

Zonder duidelijke scheiding ontstaat het risico dat:

- sensoren en verwerkende apparaten door elkaar gemodelleerd worden;
- het DC-domein (20/24) een restcategorie wordt voor “alles wat stroom gebruikt”;
- de herkomst van informatie (data-bronnen) niet meer in één oogopslag herkenbaar is;
- zekeringen en beveiliging verspreid raken over het schema.

De vraag is hoe een **heldere, consistente scheiding** wordt aangebracht tussen:

- sensoren als **beginpunten van informatie**, en
- DC-endpoints en hun **energievoorziening en beveiliging**.

---

## Beslissingscriteria

- In één oogopslag moet duidelijk zijn **waar informatie vandaan komt**.
- Het DC-domein mag **geen semantische rommelbak** worden.
- Zekeringen en CB’s moeten eenduidig te vinden zijn voor troubleshooting.
- Apparaten mogen **niet dubbel** gemodelleerd worden.
- De indeling moet toekomstvast zijn bij vervanging van apparatuuren.

---

## Overwogen opties

### Optie A — Alles onder DC distributie (24)

Alle apparaten die DC gebruiken (sensoren, displays, endpoints) worden
onder `24_DC_Distribution` gemodelleerd.

### Optie B — Sensors apart (50), DC distributie & endpoints onder 24 (gekozen)

Sensoren worden gemodelleerd als beginpunten van informatie onder `50_Sensors`.
DC-distributie, beveiliging en endpoints blijven onder `24_DC_Distribution`.

### Optie C — Sensoren fysiek onder 24, data logisch onder 50

Hybride aanpak waarin hetzelfde apparaat zowel onder DC als onder Sensors verschijnt.

---

## Besluit

**Gekozen optie: Optie B — Sensors apart, energie & endpoints centraal onder DC**
Er wordt een strikte **scheiding van verantwoordelijkheid** aangehouden:

- **50_Sensors**  
  Bevat uitsluitend **beginpunten van informatie**  
  (bijv. GPS, wind, log, diepte, heading, tankmeters).

- **24_DC_Distribution**  
  Bevat:
  - DC-distributie (rails, CB’s, zekeringen),
  - energie-voorziening naar alle apparaten,
  - en alle **DC-endpoints/verbruikers**  
    (bijv. plotters, AIS, marifoon, displays, converters).

Een sensor wordt als **sensor** gemodelleerd in 50, ook als hij DC-voeding nodig heeft.
De bijbehorende zekering of CB wordt **uitsluitend** gemodelleerd in 24.

---

## Gevolgen

### Positief

- Duidelijke semantiek: *waar komt data vandaan?* → altijd onder 50.
- DC-distributie en beveiliging zijn gecentraliseerd voor troubleshooting.
- Apparaten hoeven niet dubbel gemodelleerd te worden.
- Vervanging van endpoints (bijv. plotter, AIS) raakt de sensorarchitectuur niet.
- Schema blijft leesbaar op systeemniveau.

### Negatief

- Sommige apparaten combineren meerdere rollen (bijv. plotter met interne GPS);
  dit vraagt om expliciete rolduiding via naam of annotatie.
- Discipline vereist: sensoren niet “per ongeluk” als endpoint onder 24 tekenen
  omdat ze stroom verbruiken.

---

## Toepassing en bevestiging

Deze beslissing wordt als volgt toegepast en bewaakt:

- Onder **50_Sensors** worden alleen apparaten gemodelleerd waarvan de
  **primaire rol** datageneratie is.
- Onder **24_DC_Distribution** worden:
  - alle zekeringen en CB’s gemodelleerd,
  - inclusief de gevoede lijnen naar sensoren.
- Een sensor heeft **geen eigen DC-bron** in 50; voeding wordt altijd via 24 getoond.
- Apparaten die zowel data genereren als verwerken:
  - worden geplaatst op basis van hun **primaire rol**;
  - aanvullende rollen worden vastgelegd via naamgeving of annotatie.

---

## Notities / vervolg

- Deze ADR gaat over **conceptuele modellering**, niet over fysieke plaatsing
  of connectoren (zie ADR‑003 voor infrastructuur).
- Indien sensoren in de toekomst actief data verwerken of doorrouteren
  (bijv. edge-compute), moet hun rol opnieuw worden beoordeeld.
- De scheiding 50 ↔ 24 is normatief en geldt voor alle toekomstige uitbreidingen.
