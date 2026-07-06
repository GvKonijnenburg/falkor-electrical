# ADR-018 — Antennearchitectuur voor VHF en AIS

**Status:** Geaccepteerd
**Datum:** 2026-07-06

## Context en probleemstelling

Binnen de target-architectuur maken zowel marifonie als AIS gebruik van VHF-radiofrequenties.

Voor de fysieke antenne-architectuur bestaan twee hoofdvarianten:

- een gedeelde VHF-antenne voor marifoon en AIS;
- afzonderlijke antennes voor marifoon en AIS.

Deze keuze beïnvloedt onder meer bereik, afhankelijkheden tussen subsystemen, onderhoudbaarheid en installatiescomplexiteit.

De vraag is welke antennearchitectuur onderdeel wordt van de target-architectuur.

## Beslissingscriteria

- Betrouwbare VHF-communicatie.
- Goede AIS-ontvangst en AIS-transmissie.
- Beperking van installatiescomplexiteit.
- Beperking van fysieke componenten.
- Onderhoudbaarheid.
- Beheersbare afhankelijkheden tussen subsystemen.
- Geschiktheid voor het beoogde vaargebied.

## Overwogen opties

### Optie A — Afzonderlijke antennes voor VHF en AIS

Marifoon en AIS gebruiken elk een eigen antenne.

**Voordelen:**

- Volledige fysieke scheiding van beide subsystemen.
- Geen gedeelde RF-componenten.
- Eenvoudige foutanalyse.
- Lokale wijzigingen hebben minder invloed op andere subsystemen.

**Nadelen:**

- Extra antenne.
- Extra coaxbekabeling.
- Meer fysieke componenten.
- AIS-antenne bevindt zich vaak lager dan de primaire VHF-antenne.
- Hogere installatiecomplexiteit.

### Optie B — Gedeelde antenne voor VHF en AIS (gekozen)

Marifoon en AIS delen één VHF-antenne via een geschikte splitter.

**Voordelen:**

- Maximale antennehoogte voor zowel AIS als marifoon.
- Minder antennes.
- Minder bekabeling.
- Lagere installatiecomplexiteit.
- Eenvoudigere fysieke architectuur.

**Nadelen:**

- Introductie van een gedeelde RF-component.
- Minder fysieke scheiding tussen subsystemen.
- Uitval van de splitter kan meerdere subsystemen beïnvloeden.

### Optie C — Gedeelde antenne via geïntegreerde splitter

Marifoon en AIS delen één antenne waarbij de splitter onderdeel is van de AIS-transponder.

**Voordelen:**

- Minder afzonderlijke componenten.
- Minder bekabeling.
- Eenvoudige installatie.

**Nadelen:**

- Introductie van een apparaat met meerdere architecturale verantwoordelijkheden.
- Sterkere koppeling tussen AIS-transponder en antenne-infrastructuur.
- Vervanging van AIS-transponder beïnvloedt ook de splitterfunctie.
- Minder flexibiliteit bij toekomstige wijzigingen.

## Besluit

**Gekozen optie: Optie B — Gedeelde antenne voor VHF en AIS.**

De target-architectuur gaat uit van een gedeelde VHF-antenne voor zowel marifoon als AIS.

De voordelen van maximale antennehoogte, beperkte installatiescomplexiteit en beperking van fysieke componenten wegen zwaarder dan de nadelen van een gedeelde RF-component.

## Gevolgen

### Positief

- AIS-transponder, splitter en marifoon kunnen onafhankelijk van elkaar worden vervangen.
- Optimale antennepositie voor zowel marifoon als AIS.
- Eenvoudige fysieke architectuur.
- Beperking van componenten, bekabeling en montagepunten.
- Goede geschiktheid voor het beoogde vaargebied.

### Negatief

- Afhankelijkheid van een splitter.
- Minder fysieke scheiding tussen AIS en marifonie.
- Aanvullende aandacht nodig voor selectie van een geschikte splitter.
