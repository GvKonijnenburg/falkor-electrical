# ADR-019 — Operationeel profiel van Falkor

**Status:** Geaccepteerd  
**Datum:** 2026-07-06

## Context en probleemstelling

Architecturale keuzes binnen Falkor worden beïnvloed door het beoogde gebruik van het schip.

De target-architectuur wordt ontworpen voor particulier gebruik van Falkor en niet voor commerciële exploitatie of verhuur.

Zonder expliciete vastlegging bestaat het risico dat verschillende architectuurbesluiten uitgaan van verschillende aannames over tochtduur, zelfredzaamheid, beschikbaarheid van ondersteuning, vereiste redundantie en operationele risico's.

De vraag is voor welk operationeel profiel de target-architectuur wordt ontworpen.

## Beslissingscriteria

- Aansluiting bij het beoogde gebruik van Falkor.
- Realistische balans tussen ambitie, complexiteit en kosten.
- Ondersteuning van veilige navigatie.
- Consistente basis voor latere architectuurbesluiten.
- Voorkomen van onder- en overdimensionering van systemen.
- Ondersteuning van meerdaagse passages zonder directe toegang tot havens.
- Ondersteuning van tijdelijke zelfredzaamheid zonder ontwerp voor langdurige oceaanvaart.

## Overwogen opties

### Optie A — Dag- en weekendtochten

Falkor wordt primair ontworpen voor:

- dagtochten;
- weekendtochten;
- vaartochten waarbij dagelijks of vrijwel dagelijks een haven wordt aangelopen.

**Voordelen:**

- Lage complexiteit.
- Lage eisen aan autonomie en zelfredzaamheid.
- Lage kosten.

**Nadelen:**

- Beperkte operationele flexibiliteit.
- Minder geschikt voor langere passages.
- Sterke afhankelijkheid van havenfaciliteiten.

### Optie B — Regionale kustvaart en vakanties

Falkor wordt ontworpen voor:

- dag- en weekendtochten;
- meerdaagse tochten binnen Nederland en omliggende kustgebieden;
- vakanties waarbij regelmatig havens worden aangelopen.

**Voordelen:**

- Goede balans tussen eenvoud en flexibiliteit.
- Beperkte eisen aan autonomie.

**Nadelen:**

- Beperkte geschiktheid voor langere passages zonder tussenstops.
- Minder passend voor aanbrengtochten en prestatietochten.

### Optie C — Meerdaagse passages en offshore vaart (gekozen)

Falkor wordt ontworpen voor:

- dag- en weekendtochten;
- meerdaagse tochten binnen Nederland en omliggende kustgebieden;
- meerdaagse vakanties in buitenlandse vaargebieden;
- aanbrengtochten;
- prestatietochten;
- passages waarbij gedurende meerdere etmalen geen haven wordt aangelopen.

De architectuur moet ondersteuning bieden voor passages van meerdere etmalen zonder havenaanloop, maar hoeft niet ontworpen te worden voor langdurige afwezigheid van havens, bevoorrading of technische ondersteuning.

**Voordelen:**

- Ondersteunt een breed scala aan gebruiksscenario's.
- Goede balans tussen operationele flexibiliteit en complexiteit.
- Ondersteunt langere passages zonder directe afhankelijkheid van havenfaciliteiten.
- Sluit aan bij zowel recreatief gebruik als prestatietochten.

**Nadelen:**

- Hogere eisen aan navigatie-, communicatie- en energiesystemen.
- Hogere eisen aan zelfredzaamheid.
- Hogere complexiteit dan een puur kustgebonden ontwerp.

### Optie D — Oceaanvaart en wereldcruising

Falkor wordt ontworpen voor gebruik waarbij langdurige zelfredzaamheid buiten bereik van reguliere ondersteuning onderdeel is van het ontwerp.

Voorbeelden zijn:

- oceaanoversteken;
- wereldcruising;
- passages waarbij gedurende langere tijd geen realistische toegang bestaat tot havens, bevoorrading of technische ondersteuning.

**Voordelen:**

- Maximale operationele flexibiliteit.
- Hoge mate van autonomie en zelfredzaamheid.

**Nadelen:**

- Sterke toename van complexiteit.
- Hoge kosten.
- Zwaardere eisen aan redundantie, communicatie, energievoorziening en reserveonderdelen.

## Besluit

**Gekozen optie: Optie C — Meerdaagse passages en offshore vaart.**

De target-architectuur van Falkor wordt ontworpen voor:

- dag- en weekendtochten;
- meerdaagse tochten binnen Nederland en omliggende kustgebieden;
- meerdaagse vakanties in buitenlandse vaargebieden;
- aanbrengtochten;
- prestatietochten;
- passages waarbij gedurende meerdere etmalen geen haven wordt aangelopen.

De target-architectuur wordt niet ontworpen voor operationele profielen waarbij langdurige zelfredzaamheid buiten bereik van reguliere ondersteuning een expliciete ontwerpeis vormt.

## Gevolgen

### Positief

- Duidelijk kader voor toekomstige architectuurbesluiten.
- Voorkomt onnodige complexiteit en redundantie.
- Ondersteunt een breed maar realistisch gebruiksprofiel.
- Biedt consistente uitgangspunten voor navigatie-, communicatie- en energiesystemen.
- Ondersteunt passages waarbij tijdelijke zelfredzaamheid vereist is.

### Negatief

- Beperkt de geschiktheid voor oceaanvaart en wereldcruising.
- Toekomstige uitbreiding van het operationele profiel kan herziening van bestaande ADR's vereisen.
- Sommige keuzes die passend zijn voor oceaanvaart zullen bewust niet worden overgenomen.

## Toepassing en bevestiging

- Architectuurbesluiten worden beoordeeld in relatie tot het vastgestelde operationele profiel.
- Eisen aan beschikbaarheid, redundantie, autonomie en communicatie worden afgeleid van dit operationele profiel.
- Afwijkingen van dit operationele profiel vereisen expliciete heroverweging van de betrokken ADR's.
