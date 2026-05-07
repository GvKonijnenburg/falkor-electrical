# ADR-012 — Platformkeuze voor energie

**Status:** Geaccepteerd  
**Datum:** 2026-05-07

## Context en probleemstelling

Bij het ontwerpen van de target‑architectuur voor het elektrische systeem van Falkor staat de keuze voor een **energieplatform** centraal. Deze keuze bepaalt hoe energieopwekking, -conversie, -opslag en -distributie conceptueel worden georganiseerd en vormt daarmee een fundamenteel uitgangspunt voor de verdere systeemarchitectuur.

Binnen deze energieplatformkeuze wordt afgewogen in hoeverre functionaliteit, monitoring en besturing worden gecentraliseerd, welke mate van platformafhankelijkheid acceptabel is en hoe onderhoudbaarheid en uitbreidbaarheid op lange termijn worden gewaarborgd.

---

## Beslissingscriteria

De energieplatformkeuze wordt beoordeeld op basis van de volgende criteria:

- **Betrouwbaarheid**  
  Het platform moet voorspelbaar functioneren onder maritieme omstandigheden en geen enkelvoudige faalpunten introduceren.

- **Onderhoudbaarheid**  
  Het systeem moet begrijpelijk, diagnoseerbaar en repareerbaar blijven gedurende de volledige levensduur van het vaartuig.

- **Operationele transparantie**  
  Het platform moet inzicht geven in energiestromen, systeemstatus en foutcondities, zonder dat dit uitsluitend impliciet in configuratie of black‑box logica verborgen is.

- **Open landschap (beperking van vendor lock‑in)**  
  De mate van afhankelijkheid van één leverancier moet expliciet en beheersbaar zijn; vervanging of gedeeltelijke migratie mag de architectuur niet fundamenteel breken.

- **Architecturale evolueerbaarheid**  
  Het energieplatform moet uitbreiding en gefaseerde aanpassing mogelijk maken zonder herontwerp van het systeemmodel.

- **Integratie met het datalandschap (N2K)**  
  Het platform moet relevante energie‑ en systeeminformatie toegankelijk maken voor het bredere datalandschap, zonder dat dit het primaire doel of leidende ontwerpprincipe is.

---

## Overwogen opties

### Optie A — Victron energieplatform

Victron vormt een geïntegreerd energieplatform met een eigen communicatienetwerk (VE.Can) en een centrale controller (GX) die energiecomponenten (omvormer/lader, BMS, meetmodules, laders/regelapparatuur) samenbrengt en status/metingen ontsluit richting het datalandschap (bijv. N2K).

**Voordelen.**

- **Betrouwbaarheid:** volwassen, veel toegepaste maritieme oplossing met voorspelbaar gedrag in de praktijk.
- **Onderhoudbaarheid:** diagnose en foutanalyse zijn goed te ondersteunen door centrale monitoring en consistente tooling binnen één ecosysteem.
- **Operationele transparantie:** status, alarms, energiestromen en systeemtoestanden zijn doorgaans goed inzichtelijk te maken via GX, logging en dashboards.
- **Architecturale evolueerbaarheid:** schaalbaar binnen het ecosysteem (uitbreiden met meting, laders, BMS, etc.) zonder herontwerp van het kernmodel.
- **Integratie met datalandschap (N2K):** relatief eenvoudige ontsluiting van relevante energie-informatie richting N2K via een GX-bridge, waardoor ‘energie → data’ in de architectuur expliciet kan worden gemaakt.

**Nadelen.**

- **Open landschap / vendor lock-in:** keuze voor Victron impliceert afhankelijkheid van een leveranciers-ecosysteem en (deels) proprietary protocollen bovenop CAN.
- **Operationele transparantie (risico):** er ontstaat een verleiding om gedrag “in configuratie” te verstoppen; architecturale discipline is nodig om keuzes expliciet te houden in schema en ADR’s.
- **Architecturale evolueerbaarheid (buiten ecosysteem):** migreren naar een ander platform of combineren met niet-Victron componenten kan meer ontwerp- en integratiewerk vragen.

---

### Optie B — Mastervolt energieplatform

Mastervolt biedt eveneens een geïntegreerd energieplatform met eigen bus- en configuratiestructuren. Het platform richt zich op end-to-end energiebeheer binnen het eigen productlandschap.

**Voordelen.**

- **Betrouwbaarheid:** doorgaans solide platformgedrag binnen de eigen ecosystemische grenzen.
- **Onderhoudbaarheid:** onderhoud is goed uitvoerbaar zolang de installatie primair binnen het Mastervolt-ecosysteem blijft.
- **Architecturale evolueerbaarheid:** uitbreiden met Mastervolt componenten is mogelijk zonder fundamenteel herontwerp, mits binnen hetzelfde platform.

**Nadelen.**

- **Open landschap / vendor lock-in:** sterke afhankelijkheid van het Mastervolt-ecosysteem; uitwisseling of gedeeltelijke migratie is meestal complexer dan bij een opener aanpak.
- **Operationele transparantie:** inzicht en diagnose zijn vaak sterker gekoppeld aan leveranciersspecifieke tooling en configuratie, waardoor de architectuur minder “zelfverklarend” is vanuit schema’s alleen.
- **Integratie met datalandschap (N2K):** integratie kan mogelijk zijn, maar is minder vanzelfsprekend als primaire ontwerproute; vaak vraagt dit extra componenten of specifieke configuraties.
- **Onderhoudbaarheid (lange termijn):** afhankelijkheid van leverancier en tooling kan een risico vormen voor “future‑me”, zeker bij platformwijzigingen of beperkte beschikbaarheid.

---

### Optie C — Zelfbouw energieplatform (losse energiecomponenten)

Zelfbouw betekent het opzetten van een **eigen energieplatform** zonder
geïntegreerd commercieel ecosysteem. Energieopwekking, -opslag en -distributie
bestaan hierbij uit losse of zelf samengestelde componenten, waaronder
accucellen, BMS, laders, beveiligingen en vermogensschakelingen, die niet als
één samenhangend platform zijn ontworpen en geleverd.

De verantwoordelijkheid voor veilige en betrouwbare energielevering aan
verbruikers — inclusief foutafhandeling, begrenzing, degradatiegedrag en
onderlinge samenhang — ligt in dit scenario volledig bij het ontwerp en de
integratie door de eigenaar van het systeem.

**Voordelen.**

- Volledige controle over componentkeuze en energetische architectuur.
- Geen structurele vendor lock‑in op energieplatformniveau.
- Data‑uitwisseling kan volledig naar eigen inzicht worden opgezet.

**Nadelen.**

- Hoge complexiteit en ontwerplast voor een veiligheidskritisch energiesysteem.
- Verhoogd risico op fouten in energielevering en foutcondities.
- Structurele onderhoudsverantwoordelijkheid voor “future‑me”.
- Data‑integratie vereist expliciet ontwerp en behoud van semantiek; er is geen ingebouwde samenhang tussen energiestatus en datalandschap.

---

## Besluit

Op basis van de vastgestelde beslissingscriteria is gekozen voor een
**Victron‑gebaseerd energieplatform** (VE.Can + GX‑ecosysteem).

Deze keuze biedt de beste balans tussen:

- **Betrouwbaarheid**  
  Een geïntegreerd en in de maritieme praktijk bewezen energieplatform met
  voorspelbaar gedrag onder uiteenlopende bedrijfsomstandigheden.

- **Onderhoudbaarheid en operationele transparantie**  
  Inzicht in energiestromen, systeemstatus en foutcondities is toegankelijk
  zonder dat essentiële systeemkennis uitsluitend in impliciete configuratie
  of black‑box gedrag verborgen raakt.

- **Beheersbare afhankelijkheid van een platformleverancier**  
  Hoewel sprake is van een bewuste platformkeuze, blijft de vendor lock‑in
  expliciet, inzichtelijk en architecturaal begrensd.

- **Architecturale evolueerbaarheid**  
  Het platform ondersteunt gefaseerde uitbreiding en aanpassing van de
  energie‑architectuur zonder herontwerp van het kernmodel.

- **Integratie met het datalandschap (N2K)**  
  Relevante energie‑ en systeeminformatie kan consistent worden ontsloten
  richting het bredere datadomein, zonder dat dit de primaire drijfveer van
  het ontwerp vormt.

---

## Toepassing en bevestiging

- De gekozen energieplatformarchitectuur wordt op het top‑level schema   (`00_System`) expliciet gerepresenteerd. Het modelleren van `VE_CAN` op dit  niveau is het **zichtbare gevolg van de energieplatformkeuze** en maakt deze keuze expliciet in de systeemarchitectuur.

- Het top‑level schema drukt daarmee uit dat energieopwekking, -conversie,  -distributie en bijbehorende informatievoorziening logisch samenhangend zijn georganiseerd binnen één energieplatform, zonder implementatiedetails te specificeren.

- Concrete apparaten en technische realisaties, zoals GX‑controllers, bridges en gekoppelde componenten, worden uitgewerkt in lagere domeinen en  detailschema’s. Daar wordt vastgelegd *hoe* de energieplatformkeuze wordt  gerealiseerd, niet *of* zij bestaat.

---

## Notities / vervolg

- Deze ADR beschrijft **de platformkeuze**, niet de exacte configuratie  van individuele apparaten.
