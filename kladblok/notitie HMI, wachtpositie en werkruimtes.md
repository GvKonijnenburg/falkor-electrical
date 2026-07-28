# Notitie — HMI, wachtpositie en werkruimtes

## Aanleiding

Tijdens de discussie over de marifoonarchitectuur ontstond de vraag of Falkor een expliciete ADR nodig heeft over werkplekken, HMI of de positie van gebruikersinterfaces.

De eerste hypothese was dat de kuip de primaire operationele werkplek is en dat daarom zoveel mogelijk functies vanuit de kuip beschikbaar moeten zijn.

Bij nadere analyse blijkt deze formulering te grof en onvoldoende onderscheidend.

## Belangrijk inzicht

De plaats van een gebruikersinterface wordt niet primair bepaald door de fysieke locatie van de gebruiker, maar door de rol die een functie speelt tijdens het uitvoeren van de wacht.

De relevante vraag is niet:

> "Moet deze functie in de kuip beschikbaar zijn?"

maar:

> "Moet deze functie beschikbaar zijn zonder de wachtpositie te verlaten?"

## Waarneming uit operationeel gebruik

Tijdens normaal gebruik van Falkor bestaat de wens om de kaartentafel zo min mogelijk te bezoeken.

De kaartentafel blijft belangrijk voor:

- routeplanning;
- logboek;
- administratie;
- configuratie;
- troubleshooting;
- incidentele controle van systemen.

Tijdens een normale wacht is de voorkeur om de kuip niet te verlaten, behalve voor dergelijke niet-operationele taken.

Samengevat:

> Tijdens normaal gebruik wil ik niet naar de kaartentafel, behalve om bijvoorbeeld een kruisje op de kaart te zetten.

## Voorlopige classificatie van functies

### Wachtfuncties

Dit zijn functies die direct onderdeel uitmaken van het continu uitvoeren van de wacht.

Deze moeten beschikbaar zijn op de wachtpositie.

Voorbeelden:

- Marifoon
- Autopilot
- Plotter
- AIS-verkeersbeeld
- Diepte
- Log/snelheid
- Positie in geografische context
- Kompas
- Motorbediening
- Motorinstrumenten

Kenmerken:

- worden regelmatig of continu gebruikt;
- beïnvloeden directe beslissingen van de wachtvoerder;
- vereisen directe terugkoppeling;
- vereisen vaak direct handelingsvermogen.

### Scheepsbeheerfuncties

Dit zijn functies die betrekking hebben op het schip als systeem, maar geen integraal onderdeel vormen van het uitvoeren van de wacht.

Deze hoeven niet beschikbaar te zijn op de wachtpositie.

Voorbeelden:

- Navigatieverlichting
- Ankerlicht
- Victron GX
- Energiebeheer
- Systeemconfiguratie

Kenmerken:

- worden incidenteel gebruikt;
- zijn niet continu relevant tijdens een wacht;
- vereisen geen directe koppeling tussen waarnemen en handelen.

### Incidentele nood- of bijzondere functies

Dit zijn functies die slechts zelden worden gebruikt, maar mogelijk relevant zijn tijdens bijzondere situaties.

Voorbeelden:

- Deklicht
- Misthoorn
- Zoeklicht
- Mogelijke toekomstige MOB-functies

Bij deze functies lijkt een andere afweging te gelden.

Niet optimale plaatsing, maar:

- voorspelbaarheid;
- standaardisatie;
- vindbaarheid;
- spiergeheugen.

kunnen belangrijker zijn dan bediening op de meest optimale locatie.

Voorbeeld:

Een deklicht in de kuip kan nuttig zijn tijdens een noodsituatie, maar het is mogelijk belangrijker dat iedere opvarende exact weet waar de bediening zich bevindt dan dat deze per se buiten geplaatst is.

## Onderliggende ontwerpregel

Een mogelijke voorlopige ontwerpregel luidt:

> Functies die tijdens normaal uitvoeren van de wacht continu of regelmatig worden gebruikt moeten beschikbaar zijn op de wachtpositie.

Aanvullend:

> Functies die betrekking hebben op scheepsbeheer, configuratie of administratie hoeven niet beschikbaar te zijn op de wachtpositie.

En:

> Voor incidentele nood- of bijzondere functies kunnen voorspelbaarheid, standaardisatie en vindbaarheid zwaarder wegen dan optimale plaatsing.

## Relatie met bestaande ADR's

Deze observaties sluiten aan bij:

- ADR-019 — Operationeel profiel van Falkor
- ADR-020 — Architectuur van marifoonbediening

ADR-020 kan worden gezien als een concrete toepassing van bovenstaande gedachtegang op marifoonfunctionaliteit.

## Status

Er lijkt een consistent ontwerpprincipe te ontstaan, maar er is op dit moment nog onvoldoende onderbouwing voor een zelfstandige ADR.

Vervolgonderwerpen die mogelijk helpen dit verder scherp te krijgen:

- Alarmen
- Deklicht
- Misthoorn
- Plotterarchitectuur
- Motorbediening
- Schakelpaneel
- Toekomstige HMI-beslissingen

Op basis van toekomstige beslissingen kan worden bepaald of een afzonderlijke ADR wenselijk is.