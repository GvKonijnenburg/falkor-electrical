# ADR-015 — AIS-transmissietechnologie

**Status:** Geaccepteerd
**Datum:** 2026-07-06

## Context en probleemstelling

Binnen de target-architectuur moeten andere schepen Falkor via AIS kunnen identificeren en volgen.

AIS-transponders zijn verkrijgbaar in verschillende klassen. Class A is primair bedoeld voor beroepsvaart en grotere schepen waarvoor AIS verplicht is. Voor een zeiljacht als Falkor wordt daarom uitsluitend gekeken naar Class B-transponders.

Voor AIS Class B transponders bestaan twee transmissiemechanismen:

- CSTDMA (Carrier Sense Time Division Multiple Access);
- SOTDMA (Self-Organized Time Division Multiple Access).

Beide zijn compatibel met het AIS-ecosysteem, maar verschillen in de manier waarop zendtijdslots worden verkregen en behouden, met gevolgen voor zichtbaarheid en prestaties bij hoge verkeersdichtheid.

De vraag is welke transmissietechnologie onderdeel wordt van de target-architectuur.

## Beslissingscriteria

- Goede zichtbaarheid voor andere schepen.
- Voorspelbaar gedrag bij hoge verkeersdichtheid.
- Geschiktheid voor kustvaart, offshore gebruik en drukke verkeersgebieden.
- Toekomstvastheid van de architectuur.
- Vermijden van keuzes die primair worden gedreven door aanschafprijs.

## Overwogen opties

### Optie A — Class B CSTDMA

Traditionele Class B AIS-transponders gebruiken CSTDMA.

**Voordelen.**

- Lagere aanschafkosten.
- Brede compatibiliteit.

**Nadelen.**

- Lagere zendprioriteit.
- Minder voorspelbaar gedrag bij hoge verkeersdichtheid.
- Beschouwd als de instapvariant binnen AIS-transponders.

### Optie B — Class B SOTDMA (gekozen)

Class B SOTDMA-transponders reserveren actief toekomstige tijdslots.

**Voordelen.**

- Hogere zendprioriteit.
- Voorspelbaarder gedrag bij hoge verkeersdichtheid.
- Beter passend bij een moderne installatie.
- Breed ondersteund door actuele AIS-productlijnen.

**Nadelen.**

- Hogere aanschafkosten.

## Besluit

**Gekozen optie: Optie B — Class B SOTDMA.**

Nieuwe AIS-transponders binnen de target-architectuur moeten
SOTDMA ondersteunen.

CSTDMA wordt niet toegepast als primaire AIS-transmissietechnologie.

## Gevolgen

### Positief

- Hogere zichtbaarheid voor andere schepen.
- Betere prestaties in drukke vaargebieden.
- Toekomstvaste AIS-architectuur.
- Verminderd risico op beperkingen door verkeersdichtheid.

### Negatief

- Hogere aanschafkosten.
- Kleinere productselectie dan bij alle beschikbare Class B-oplossingen samen.

## Toepassing en bevestiging

- Bij selectie van een AIS-transponder is SOTDMA een harde eis.
- Producten die uitsluitend CSTDMA ondersteunen vallen af.
- Verdere keuzes omtrent antennes, displays, marifoons en specifieke apparatuur vallen buiten de scope van deze ADR.

## Notities / vervolg

- De keuze voor SOTDMA legt geen specifieke leverancier of productlijn vast.
- Presentatie van AIS-informatie wordt behandeld in een afzonderlijke ADR.
- De relatie tussen AIS-transponder, marifoon en eventuele aanvullende AIS-ontvangers wordt behandeld in een afzonderlijke ADR.
