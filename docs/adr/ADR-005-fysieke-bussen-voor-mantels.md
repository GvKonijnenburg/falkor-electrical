# ADR-005 — Gebruik van fysieke bussen voor mantels

**Status:** Geaccepteerd  
**Datum:** 2026-05-05

## Context en probleemstelling

In het schema komen meerdere situaties voor waarin één fysieke mantel/loom meerdere aders bevat (bijv. walstroomkabel met L/N/PE, mastbekabeling voor toplichten en deklicht). Zonder bundeling wordt het top-level (00) snel visueel druk en wordt fysieke realiteit (“één kabel”) niet goed zichtbaar. KiCad ondersteunt bussen op meerdere manieren (platte bus vs geneste bus). De vraag is wanneer we een bus gebruiken en welke KiCad bus-notatie we hanteren, zodat de semantiek van aders zuiver blijft en de modellering zowel functioneel als fysiek begrijpelijk is.

## Beslissingscriteria

- Een bus representeert een fysiek kabelobject (mantel/loom), niet alleen cosmetische bundeling.
- Fundamentele nets (zoals AC_L/AC_N/PE) behouden hun zelfstandige betekenis.
- De oplossing verbetert leesbaarheid op 00 zonder “magie” of het suggereren van nieuwe netwerken.
- De oplossing is consistent toepasbaar op mast-looms en andere fysieke bundels.
- Schakeling en beveiliging moeten elektrisch correct op de juiste geleiders worden gemodelleerd, zonder dat een bus onterecht suggereert dat alle aders hetzelfde gedrag hebben.

## Overwogen opties

### Optie A — Geneste bus-notatie (BUS{...})

Aders krijgen gescopede namen zoals AC_IN.AC_L.

### Optie B — Platte bus-notatie (BUS = {...}) (gekozen)

De bus bundelt bestaande nets met zelfstandige betekenis, bijvoorbeeld AC_IN = { AC_L, AC_N, PE }.

### Optie C — Geen bus; losse aders tekenen

L/N/PE en mast-aders worden als losse verbindingen tussen bladen getekend.

## Besluit

**Gekozen optie: Optie B — Platte bus-notatie voor fysieke mantels.** Een bus wordt alleen gebruikt wanneer er fysiek een mantel/loom is. De bus bundelt bestaande nets; de aders behouden hun eigen netnaam. De geneste notatie (bijv. AC_IN.AC_L) wordt vermeden, omdat die een kunstmatige naamruimte introduceert die niet past bij “bus = fysieke mantel”.

**Aanvullende regel: schakelaars en circuitbreakers worden gemodelleerd op individuele geleiders, niet op de bus als geheel.** De bus blijft het model van de fysieke mantel; je onderbreekt alleen de nets die in werkelijkheid worden geschakeld of beveiligd. Dit betekent expliciet dat we de bus niet “helemaal stoppen en opnieuw opbouwen” rond een schakelaar; we halen alleen de betreffende ader(s) uit de bus en modelleren die als losse net(s) door het schakelobject heen, waarna ze weer als net terug in de bundel begrepen worden.

Concreet voor AC is dit de default: een schakelaar of automaat zit op AC_L; AC_N en PE lopen elektrisch door. Voor een 2-polige automaat kunnen AC_L en AC_N beide door schakelcontacten lopen; PE blijft altijd ononderbroken.

## Voorbeelden

**Voorbeeld walstroom (AC):** Op 00 staat connector J_SHORE_AC met nets AC_L, AC_N en PE. De busdefinitie is AC_IN = { AC_L, AC_N, PE }. Naar 10_Power_AC loopt één busverbinding AC_IN.

**Voorbeeld mast (DC):** Per mantel/connector een eigen bus, bijvoorbeeld MAST_TOP = { MAST_3COL_POS, MAST_ANCHOR_POS, MAST_TOP_NEG } en MAST_DECK = { MAST_DECK_POS, MAST_DECK_NEG }.

**Voorbeeld schakelaar in AC_L (bus blijft bestaan):** AC_IN = { AC_L, AC_N, PE } loopt als fysieke mantel, maar de schakelaar Qx zit alleen in AC_L. In het schema teken je AC_L als losse net door Qx en laat je AC_N en PE ononderbroken doorlopen. Je modelleert dus niet “AC_IN door Qx”, maar alleen “AC_L door Qx”.

**Voorbeeld circuitbreaker (automaat) in AC_L:** Voor een 1-polige automaat modelleer je AC_L → Qx → AC_L_PROTECTED; AC_N en PE lopen door. Voor een 2-polige automaat modelleer je AC_L → QxA → AC_L_PROTECTED en AC_N → QxB → AC_N_PROTECTED; PE loopt door.

## Gevolgen

### Positief

- 00 blijft compact: één mantel = één verbinding.
- Aders behouden semantiek (PE blijft PE; geen AC_IN.PE).
- Consistent patroon voor alle fysieke bundels (mast, walstroom, etc.).
- Schakeling en beveiliging worden elektrisch correct gemodelleerd per geleider, zonder dat een bus suggereert dat alle aders hetzelfde gedrag hebben.
- PE-continuïteit blijft zichtbaar doordat PE niet “meeschakelt” in bus-abstracties.

### Negatief

- Discipline nodig: bus alleen gebruiken als er echt één mantel is.
- Bij wijziging in loom-samenstelling moet de busdefinitie worden bijgewerkt.
- Het “uithalen” van één ader uit een bus rond een schakelaar kan extra tekenwerk geven, maar dit is bewust gekozen voor elektrische correctheid en leesbaarheid.

## Toepassing en bevestiging

- In reviews geldt: bus = fysieke mantel/loom.
- Bus-notatie is altijd “plat” (BUS = { NET1, NET2, ... }).
- Geneste bus-notatie wordt alleen toegestaan na expliciete ADR-wijziging.
- Schakelaars, relaiscontacten en circuitbreakers worden altijd op individuele nets gemodelleerd; een bus wordt niet als geheel door een schakelobject geleid.
- Voor AC geldt standaard: alleen AC_L wordt geschakeld, AC_N en PE lopen door; afwijkingen (bijv. 2-polige automaat) worden expliciet gemodelleerd.

## Notities / vervolg

- Voor RF coax wordt geen bus gebruikt; coax is één signaalpad met shield (indien gemodelleerd).
- Voor N2K/VE_CAN blijven netlabels leidend; fysieke topologie wordt in 60 beschreven (ADR-003).
