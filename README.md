# Falkor Electrical

Deze repository bevat de **elektrische systeemarchitectuur en bijbehorende documentatie**
voor het zeiljacht **Falkor**.

De repository is opgezet als een **langlevend technisch referentiepunt** voor:

- ontwerp en refit-planning,
- gefaseerde uitvoering,
- troubleshooting van de geïnstalleerde situatie,
- en onderhoud door *future me*.

Architecturale beslissingen zijn expliciet vastgelegd in ADR’s
en worden **niet impliciet afgeleid uit schema’s of directorystructuur**.

---

## Wat is dit (wel)?

- De **bron van waarheid** voor het elektrische ontwerp van Falkor
- Een KiCad-project met top-down architectuur
- Een Git-repository met expliciete ontwerpbeslissingen (ADR’s)
- Een hulpmiddel om *bedoelde architectuur* en *werkelijkheid* uit elkaar te houden

---

## Wat is dit niet?

- Geen logboek van klusjes of tijdelijke wijzigingen
- Geen verzameling exports (Gerbers/PDF’s)
- Geen duplicaat van besluitvorming die al in ADR’s is vastgelegd

---

## Hoe deze repository gebruikt wordt

### 1. Architectuur en schema’s

Het KiCad-project beschrijft de **bedoelde (target) architectuur**.
De betekenis van lagen, nummering en modellering is vastgelegd in ADR’s.

→ Zie `docs/adr/`

### 2. Huidige situatie (as-is)

De feitelijke, geïnstalleerde situatie wordt vastgelegd via **Git-snapshots**
(`current/as-is-YYYY-MM` branches).

Deze branches zijn bedoeld voor:

- troubleshooting,
- terugkijken naar eerdere situaties,
- niet voor ontwerpbesluiten.

### 3. Ontwerpbeslissingen

Alle **normatieve keuzes** over:

- werkwijze,
- nummering,
- modellering,
- netwerken,
- apparaten

liggen vast in **Architecture Decision Records (ADR’s)**.

De README herhaalt deze beslissingen bewust **niet**.

---

## Waar vind ik wat?

- **KiCad-project**  
  → `kicad/`

- **Architecture Decision Records (ADR’s)**  
  → `docs/adr/`  
  Start hier om het *waarom* achter het ontwerp te begrijpen.

- **Architectuuroverzicht in woorden**  
  → `docs/Architecture.md` (optioneel narratief)

- **Uitvoeringsfasen / plateaus**  
  → `docs/Migration.md`

- **Genereerbare outputs (niet in Git)**  
  → `exports/` (lokaal)

---

## Leesadvies (belangrijk)

Voor begrip van het systeem:

1. Lees eerst de ADR’s onder **Fundament & werkwijze**
2. Daarna **Modellering & schema‑grammatica**
3. Vervolgens **Netwerken & communicatie**
4. Tot slot **Apparaten & concrete keuzes**

De actuele indeling staat in `docs/adr/ADR-INDEX.md`.

---

## Doelgroep

Primair bedoeld voor:

- de eigenaar van Falkor (nu en later)

Vereiste voorkennis:

- basis maritieme elektrische systemen
- KiCad
- Git

---

## Richtlijn (voor future me)

> Ontwerp beschrijft intentie.  
> Snapshots beschrijven werkelijkheid.  
> ADR’s beschrijven besluiten.  
> Git bewaart alles.
