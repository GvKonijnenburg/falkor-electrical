# ADR-020 — Architectuur van marifoonbediening

**Status:** Geaccepteerd  
**Datum:** 2026-07-28

## Context en probleemstelling

Binnen de target-architectuur moet marifonie beschikbaar zijn voor communicatie met andere schepen, nautische diensten en noodverkeer.

Voor de architectuur van marifoonbediening bestaan grofweg drie varianten:

- een traditionele marifoon die uitsluitend vanaf de kaartentafel wordt bediend;
- een traditionele marifoon met een aanvullend bedieningsstation in de kuip;
- een black-box marifoon waarbij de radio-unit los staat van de gebruikersinterface.

Deze keuze beïnvloedt onder meer de operationele bruikbaarheid tijdens het varen, de locatie van de primaire gebruikersinterface, de cognitieve belasting van de wachtvoerder en de wijze waarop apparatuur wordt beschermd tegen weersinvloeden.

Uit ADR-019 volgt dat Falkor wordt ontworpen voor meerdaagse passages en offshore vaart. Het operationele gebruik vindt daarbij primair plaats vanuit de kuip, terwijl de kaartentafel een ondersteunende functie vervult.

De vraag is welke architectuur voor marifoonbediening onderdeel wordt van de target-architectuur.

## Beslissingscriteria

- Aansluiting bij het operationeel profiel van Falkor.
- Volledige marifoonfunctionaliteit beschikbaar op de primaire operationele werkplek.
- Lage cognitieve belasting.
- Consistente bediening van de marifoon.
- Bescherming van apparatuur tegen weersinvloeden.
- Onderhoudbaarheid.
- Beheersbare complexiteit.
- Onafhankelijkheid van specifieke leveranciers of producten.

## Overwogen opties

### Optie A — Marifoon bediend vanaf kaartentafel

De marifoon wordt geplaatst en bediend vanaf de kaartentafel.

**Voordelen:**

- Eenvoudige installatie.
- Lage kosten.
- Groot aanbod aan geschikte apparatuur.

**Nadelen:**

- Primaire bediening bevindt zich niet op de operationele werkplek.
- Bediening vanuit de kuip vereist verplaatsing naar binnen of gebruik van een handheld-marifoon.
- Sluit minder goed aan bij het feitelijke gebruikspatroon van Falkor.

### Optie B — Marifoon bij kaartentafel met aanvullend bedieningsstation

De marifoon wordt geplaatst bij de kaartentafel en uitgebreid met een tweede bedieningsstation in de kuip.

**Voordelen:**

- Bediening beschikbaar op meerdere locaties.
- Volwaardige marifoon blijft aanwezig bij de kaartentafel.
- Breed beschikbaar productaanbod.

**Nadelen:**

- Architectuur blijft primair gebaseerd op een hoofdstation binnen.
- Mogelijke verschillen tussen de gebruikersinterfaces van hoofd- en nevenstation.
- Hogere complexiteit.

### Optie C — Black-box marifoon met remote stations (gekozen)

De radio-unit wordt onafhankelijk van de gebruikersinterface geplaatst.

Bediening vindt plaats via één of meer remote stations op de locaties waar de marifoon daadwerkelijk wordt gebruikt.

**Voordelen:**

- Primaire bediening kan in de kuip worden geplaatst.
- Radio-unit kan droog en beschermd worden opgesteld.
- Consistente gebruikersinterface op meerdere locaties.
- Goede aansluiting op het operationele gebruik van Falkor.
- Flexibele plaatsing van bedieningslocaties.

**Nadelen:**

- Hogere kosten.
- Extra bekabeling tussen radio-unit en bedieningsstations.
- Grotere afhankelijkheid van remote bediening.

## Besluit

**Gekozen optie: Optie C — Black-box marifoon met remote stations.**

De target-architectuur gaat uit van een marifoonarchitectuur waarbij:

- de radio-unit onafhankelijk van de gebruikersinterface wordt geplaatst;
- de primaire bedieningslocatie zich in de kuip bevindt;
- aanvullende bedieningslocaties mogelijk zijn;
- handheld-marifoons niet worden beschouwd als onderdeel van de primaire marifoonarchitectuur.

## Gevolgen

### Positief

- De primaire marifoonbediening bevindt zich op de operationele werkplek van de wachtvoerder.
- Apparatuur kan beschermd en droog worden opgesteld.
- De architectuur sluit aan bij het operationele profiel van Falkor.
- Productselectie kan plaatsvinden zonder afhankelijkheid van een specifieke locatie van de radio-unit.
- Consistente bediening vermindert de cognitieve belasting.

### Negatief

- Traditionele marifoons zonder geschikte remote-bedieningsmogelijkheden passen minder goed binnen de target-architectuur.
- Hogere kosten dan de eenvoudigste marifoonoplossingen.
- Extra afhankelijkheid van bekabeling tussen radio-unit en bedieningsstations.

## Toepassing en bevestiging

- Nieuwe marifoonoplossingen worden beoordeeld op hun geschiktheid binnen een black-box architectuur.
- De primaire bedieningslocatie wordt beschouwd als onderdeel van de kuipomgeving.
- Productkeuzes voor marifoons worden afgeleid van deze architectuur en niet andersom.

## Notities / vervolg

- Relaties met AIS vallen onder ADR-015, ADR-016, ADR-017 en ADR-018.
- Dataplatformkeuzes vallen onder ADR-006 en ADR-014.
- Het operationeel profiel valt onder ADR-019.
