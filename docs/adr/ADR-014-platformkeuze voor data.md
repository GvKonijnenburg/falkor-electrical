# ADR-014 — Platformkeuze voor data

**Status:** Geaccepteerd  
**Datum:** 2026-05-11

## Context en probleemstelling

In de systeemarchitectuur van Falkor speelt uitwisseling van meetgegevens en statusinformatie tussen sensoren, subsystemen en gebruikersinterfaces een centrale rol. Deze gegevens worden gebruikt voor navigatie, monitoring en inzicht door de gebruiker.

Er bestaan meerdere mogelijke dataplatformen en transportmechanismen, zoals analoge signalen, NMEA 0183, NMEA 2000 en verschillende vendor‑specifieke databussen (bijv. SeaTalk). Zonder expliciete platformkeuze ontstaat het risico op ad‑hoc oplossingen, toenemende complexiteit en verminderde onderhoudbaarheid.

Deze ADR legt vast welk dataplatform in de target‑architectuur als primair uitwisselingsmechanisme wordt gebruikt en welke expliciete grenzen daarbij gelden.

## Beslissingscriteria

De keuze voor een dataplatform wordt beoordeeld op basis van:

- **Interoperabiliteit**  
  Compatibiliteit met gangbare maritieme sensoren, displays en   navigatie‑apparatuur.

- **Robuustheid en beschikbaarheid**  
  Uitval van het dataplatform mag geen directe impact hebben op   veiligheidskritische functies zoals starten of laden.

- **Architecturale eenvoud**  
  Eén duidelijk primair dataplatform heeft de voorkeur boven meerdere parallelle   transportsystemen.

- **Toekomstvastheid**  
  Brede ondersteuning door meerdere leveranciers en langdurige beschikbaarheid in de maritieme sector.

- **Beheersbare complexiteit**  
  Datastromen moeten begrijpelijk blijven en goed te diagnosticeren zijn tijdens onderhoud en troubleshooting.

## Overwogen opties

### Optie A — Gemengde aanpak zonder primair platform

Combinatie van analoge signalen, NMEA 0183 en lokale busverbindingen.

**Nadelen.**

- Fragmentatie van datastromen.
- Moeilijk te onderhouden en uit te breiden.
- Geen duidelijke architecturale ruggengraat.

---

### Optie B — NMEA 0183 als primair dataplatform

Seriële punt‑tot‑punt datacommunicatie.

**Nadelen.**

- Beperkte bandbreedte en schaalbaarheid.
- Verouderde standaard voor complexe en groeiende systemen.

---

### Optie C — NMEA 2000 als primair dataplatform (gekozen)

Gestandaardiseerd CAN‑gebaseerd netwerk voor maritieme data‑uitwisseling.

**Voordelen.**

- Brede ondersteuning door sensoren, displays en navigatie‑apparatuur.
- Eén gedeeld datalandschap voor navigatie‑, status‑ en alarmsignalen.
- Leveranciersoverstijgend en breed geaccepteerd.

**Beperkingen.**

- N2K is primair informatief van aard.
- Beperkingen in updatefrequentie en latency voor snelle regel‑ en  veiligheidskritische functies.

---

### Optie D — Vendor‑specifieke dataplatformen (SeaTalk, EVC, CZone e.d.)

Gebruik van proprietary platformen van individuele leveranciers, zoals:

- Raymarine (SeaTalk / SeaTalkng)
- Volvo Penta (EVC)
- Mercury (SmartCraft)
- Digitale schakelsystemen met eigen CAN‑varianten

**Voordelen.**

- Diepe integratie binnen één leveranciersecosysteem.
- Volledige ondersteuning van vendor‑specifieke functies.

**Nadelen.**

- Sterke vendor lock‑in.
- Beperkte interoperabiliteit.
- Architectuur en datamodel zijn niet transparant of vrij uitbreidbaar.
- Minder geschikt als generiek dataplatform voor het totale systeem.

## Besluit

In de target‑architectuur wordt **NMEA 2000 (N2K)** gekozen als primair dataplatform voor de uitwisseling van sensorgegevens en systeemstatus.

Vendor‑specifieke dataplatformen (zoals SeaTalk) worden niet als primair systeemplatform ingezet. Zij kunnen optioneel voorkomen als interne of afgeleide implementatielaag binnen specifieke apparatuur, mits hun gegevens
(expliciet of via gateways) worden ontsloten naar het N2K‑datalandschap.

N2K wordt niet gebruikt als directe besturingslaag voor veiligheidskritische functies, waaronder:

- starten van de motor;
- schakelen van start‑ en laadrelais.

Deze functies blijven lokaal en bus‑onafhankelijk operationeel.

## Gevolgen

### Positief

- Eenduidig en consistent datalandschap.
- Maximale interoperabiliteit met maritieme apparatuur.
- Eenvoudige uitbreiding van sensoren en displays.
- Goede mogelijkheden voor monitoring en diagnose.

### Negatief

- Mogelijke bandbreedte‑ en latencybeperkingen bij snelle regelkringen.
- Hogere kosten voor sommige sensoren of gateways.
- Afhankelijkheid van correcte N2K‑topologie en terminatie.

## Toepassing en bevestiging

- In de initial target publiceren alle sensoren hun gegevens via N2K.
- Eventuele afwijkingen (bijv. lokale sensorverbindingen of directe koppelingen met autopilotlogica) worden in een latere fase beoordeeld op basis van prestaties, robuustheid en complexiteit.
- Het wegvallen van N2K mag nooit leiden tot verlies van basale functionaliteit  zoals starten of laden.

## Notities / vervolg

- In een latere fase wordt per sensorcategorie beoordeeld of N2K technisch en functioneel geschikt is (updatefrequentie, latency en foutgedrag).
- Eventuele vendor‑specifieke optimalisaties worden expliciet afgewogen tegen interoperabiliteit en onderhoudbaarheid.
- Deze ADR beschrijft de architecturale intentie, niet de uiteindelijke fysieke implementatie.
