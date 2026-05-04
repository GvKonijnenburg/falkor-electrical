# ADR-007 — VE.Can als ownerless netwerk + Cerbo GX als bridge naar N2K

**Status:** Geaccepteerd  
**Datum:** 2026-05-01

---

## Context en probleemstelling

In de target-architectuur bestaat een Victron VE.Can netwerk (VE_CAN) en een NMEA2000 netwerk (N2K).
Een Cerbo GX (target) vormt de bridge: Victron data (o.a. MultiPlus II, Lynx BMS) wordt
beschikbaar op N2K.

De vraag is hoe VE_CAN en de bridge worden gemodelleerd zodat:

- de communicatie zichtbaar is op 00 zonder afhankelijk te zijn van 60;
- VE_CAN geen onjuist eigenaarschap krijgt (niet “van AC” of “van DC”);
- fysieke topologie (daisy chain) toch gedocumenteerd blijft.

---

## Beslissingscriteria

- 00 toont deelname aan netwerken en bridges (functionele relaties), geen topologie.
- VE_CAN heeft geen functionele eigenaar; het is infrastructuur.
- AC/DC facades blijven zuiver als energiecontract (geen netwerk-eigenaarschap).
- Fysieke implementatie wordt onder 60 beschreven (ADR-003), zonder device duplicatie.

---

## Overwogen opties

### Optie A — VE_CAN als contract-sheet-pin van energie-facades

VE_CAN als onderdeel van 10/20 contract.

### Optie B — VE_CAN als logisch net op 00; ownerless; topologie in 60 (gekozen)

Devices hebben VE_CAN poort; 00 toont deelname; 60 beschrijft daisy chain.

### Optie C — VE_CAN alleen in 60

Communicatie alleen zichtbaar in infrastructuurlaag.

---

## Besluit

**Gekozen optie: Optie B — VE_CAN is ownerless en zichtbaar als logisch net op 00.**

- `VE_CAN` wordt op 00 gemodelleerd als logisch netlabel tussen deelnemende devices.
- `VE_CAN` heeft geen eigenaar; het netwerk zelf is infrastructuur.
- Cerbo GX wordt op 00 als **bridge-projectie** getoond met uitsluitend de poorten:
  - `VE_CAN`
  - `N2K`
  (geen DC-in, tank inputs, etc. op 00).
- Fysieke daisy-chain/topologie van VE_CAN wordt in `63_VE_CAN` onder 60 gedocumenteerd
  met taps/connectorpunten (geen duplicatie van devices).

---

## Gevolgen

### Positief

- In één oogopslag zichtbaar op 00: MultiPlus/Cerbo/Lynx participeren op VE_CAN.
- Bridge VE_CAN ↔ N2K is expliciet en functioneel begrijpelijk.
- AC/DC facades blijven zuiver (energie, geen netwerk-eigenaarschap).
- Fysieke topologie blijft toch traceerbaar in 60.

### Negatief

- Discipline nodig om VE_CAN sheet-pins op facades niet als “eigenaarschap” te interpreteren.
- Cerbo GX moet consequent als bridge-projectie gemodelleerd worden (alleen netwerkpoorten).

---

## Toepassing en bevestiging

- Op 00 bestaat een logisch netlabel `VE_CAN` dat alle deelnemende devices verbindt.
- Cerbo GX wordt op 00 alleen als bridge getoond met `VE_CAN` en `N2K`.
- In 60/63_VE_CAN:
  - geen devices dupliceren;
  - alleen taps/connectorpunten met verwijzing naar device-ID.
- VE_CAN topologie (terminators, volgorde) wordt hier onderhouden.

---

## Notities / vervolg

- VE_CAN wordt fysiek anders aangelegd dan N2K (daisy-chain vs backbone). Dit verschil is
  implementatie en hoort onder 60.
- Indien later meerdere VE_CAN segmenten ontstaan, wordt dit vastgelegd in een nieuwe ADR.
