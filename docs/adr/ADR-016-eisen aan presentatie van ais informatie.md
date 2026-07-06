# ADR-016 — Eisen aan presentatie van AIS-informatie

**Status:** Geaccepteerd
**Datum:** 2026-07-06

## Context en probleemstelling

Binnen de target-architectuur moeten bemanning en wachtvoerder AIS-informatie kunnen gebruiken voor situational awareness en verkeersveiligheid. AIS-informatie kan via verschillende gebruikersinterfaces worden gepresenteerd. Deze presentatiekanalen verschillen in functionaliteit, beschikbaarheid en gebruiksgemak. Zonder expliciete eisen bestaat het risico dat keuzes voor AIS-apparatuur, displays en integraties worden gemaakt zonder een gedeeld beeld van welke informatiebehoeften ondersteund moeten worden.

De vraag is welke eisen de target-architectuur stelt aan de presentatie van AIS-informatie.

## Beslissingscriteria

- Ondersteuning van veilige navigatie.
- Situational awareness tijdens normaal gebruik.
- Situational awareness bij slecht weer en hoge verkeersdichtheid.
- Beschikbaarheid van AIS-informatie bij uitval van individuele componenten.
- Onafhankelijkheid van specifieke leveranciers of producten.
- Beheersbare complexiteit.
- Toekomstvastheid van de architectuur.

## Overwogen opties

### Optie A — Geen expliciete eisen

Eisen worden impliciet afgeleid uit de mogelijkheden van gekozen apparatuur.

**Voordelen:**

- Maximale flexibiliteit.
- Geen aanvullende architectuurregels.

**Nadelen:**

- Architectuur wordt afhankelijk van productkeuzes.
- Moeilijk toetsbaar.
- Risico op onvoldoende situational awareness.
- Risico op onvoldoende fallback-mogelijkheden.

### Optie B — Minimale presentatie-eisen definiëren (gekozen)

De architectuur legt vast welke informatie beschikbaar moet zijn en welke informatiebehoeften ondersteund moeten worden.

**Voordelen:**

- Productkeuzes kunnen objectief worden beoordeeld.
- Vereiste functionaliteit wordt expliciet.
- Toekomstige vervanging van apparatuur blijft mogelijk.
- Situational awareness wordt als capability geborgd.

**Nadelen:**

- Vereist onderhoud van de gestelde eisen.
- Kan leiden tot aanvullende eisen aan systemen of integraties.

## Besluit

**Gekozen optie: Optie B — Minimale presentatie-eisen definiëren.**

De target-architectuur definieert eisen voor de beschikbaarheid en presentatie van AIS-informatie, onafhankelijk van concrete apparatuur.

## Eisen

### Verkeerssituatie rondom Falkor

De gebruiker moet in één oogopslag inzicht kunnen krijgen in de verkeerssituatie rondom Falkor. Deze eis geldt expliciet ook onder omstandigheden waarin langdurige interactie met de gebruikersinterface ongewenst is, zoals:

- slecht weer;
- nachtelijke navigatie;
- hoge verkeersdichtheid.

Het analyseren van de verkeerssituatie mag niet afhankelijk zijn van het individueel inspecteren van AIS-targets.

Deze capability wordt ingevuld door:

- relatieve verkeersweergave;
- conflictanalyse.

#### Relatieve verkeersweergave

AIS-targets moeten zichtbaar gemaakt kunnen worden in een relatieve weergave ten opzichte van Falkor. De gebruiker moet hierbij in één oogopslag kunnen bepalen:

- waar andere schepen zich bevinden;
- hoe ver deze schepen verwijderd zijn;
- aan welke zijde van Falkor deze schepen zich bevinden.

Een radarachtige presentatie met afstandsringen voldoet aan deze eis.

Een uitsluitend tekstuele targetlijst voldoet niet aan deze eis.

#### Conflictanalyse

De gebruiker moet AIS-targets kunnen beoordelen op aanvaringsrisico. Ten minste de volgende informatie moet beschikbaar zijn:

- CPA (Closest Point of Approach);
- TCPA (Time to Closest Point of Approach).

Daarnaast moet een targetlijst beschikbaar zijn die ten minste geordend kan worden op:

- afstand;
- CPA;
- TCPA.

### Geografische context

De gebruiker moet AIS-targets kunnen beoordelen in hun geografische context.

AIS-targets moeten daarom zichtbaar gemaakt kunnen worden in combinatie met geografische informatie zoals:

- kaartinformatie;
- vaargeulen;
- verkeersscheidingsstelsels (TSS);
- havens en havenaanlopen;
- route-informatie.

Een kaartweergave met AIS-overlay voldoet aan deze eis.

### Doeldetails

Voor individuele AIS-targets moeten ten minste de volgende gegevens beschikbaar zijn:

- schipnaam (indien beschikbaar);
- MMSI;
- positie;
- koers;
- snelheid;
- CPA;
- TCPA.

### Operationele beschikbaarheid

AIS-informatie moet beschikbaar zijn via gebruikersinterfaces die tijdens normaal gebruik direct beschikbaar zijn voor de wachtvoerder.

## Gevolgen

### Positief

- Duidelijke basis voor toekomstige apparaatkeuzes.
- Scheiding tussen requirements en implementatie.
- Verminderd risico op impliciete aannames.
- Situational awareness wordt expliciet onderdeel van de architectuur.

### Negatief

- Niet alle eisen zijn op dit moment volledig uitgewerkt.
- Verdere ADR's zijn nodig om de architectuur concreet uit te werken.

## Toepassing en bevestiging

- Nieuwe apparaatkeuzes worden getoetst aan de in deze ADR vastgelegde eisen.
- Latere ADR's mogen aanvullende eisen toevoegen, maar mogen deze basisvereisten niet verzwakken zonder expliciet besluit.
- Bij beoordeling van AIS-functionaliteit staat situational awareness centraal, niet uitsluitend de beschikbaarheid van ruwe AIS-data.

## Notities / vervolg

- De wijze waarop AIS-informatie over verschillende gebruikersinterfaces wordt verdeeld valt buiten de scope van deze ADR.
- Eventuele eisen ten aanzien van AIS-alarmering worden in een afzonderlijke ADR behandeld.
