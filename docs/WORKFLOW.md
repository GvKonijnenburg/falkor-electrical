# Werkwijze – Falkor Electrical (normatief)

Dit document beschrijft de **normatieve werkwijze** voor het ontwikkelen en
onderhouden van de elektrische systeemarchitectuur van Falkor.

Het doel van dit document is **discipline en consistentie**:
het legt vast *wanneer* iets mag, *onder welke voorwaarden* en *wat leidend is*.

Architecturale keuzes zelf worden normatief vastgelegd in ADR’s (`docs/adr/`).
Dit document beschrijft **niet** de inhoud van die keuzes.

---

## Leidende uitgangspunten

- De **target‑architectuur** is leidend en beschrijft de bedoelde eindsituatie.
- De **as‑is situatie** beschrijft de feitelijke installatie op een specifiek moment.
- Deze twee waarheden worden **expliciet gescheiden**.
- Alle blijvende keuzes zijn **herleidbaar tot ADR’s**.

---

## Werken aan de target‑architectuur

Ontwerpwerk aan de target gebeurt uitsluitend:

- vanuit `main`,
- in een aparte **feature branch**,
- en alleen binnen de kaders van de geldende ADR’s.

De target wordt eerst uitgewerkt op **architectuurniveau**:
rollen, domeinen, netwerken en systeemgrenzen.
Detailengineering is expliciet *geen* vereiste op dit niveau.

---

## Wanneer mag een feature branch naar `main`?

Een feature branch mag worden gemerged naar `main` wanneer de target
**beslissingsrijp** is.

Dat betekent dat aan **alle** onderstaande criteria is voldaan:

### Architectuur

- Alle benodigde architecturale domeinen bestaan.
- Er zijn geen open vragen die alleen door herstructurering zijn op te lossen.
- Nieuwe domeinen zouden alleen via een nieuwe ADR ontstaan.

### Top‑level (00)

- `00_TopLevel` is logisch compleet en stabiel.
- Netwerken, subsystemen en bridges zijn expliciet zichtbaar.
- Verdere detaillering kan plaatsvinden **zonder wijziging van 00**.

### Abstractieniveau

- Onderdelen staan op het juiste niveau:
  - geen kabeltopologie buiten 60,
  - geen zekeringen buiten 24,
  - geen apparaten op 00.
- Er is geen “tijdelijke” plaatsing van componenten.

### Besluitdekking

- Alle gemaakte keuzes zijn gedekt door bestaande ADR’s.
- Er bestaan geen impliciete of ongedocumenteerde besluiten.

### Detailvrijheid

- Kabeldiktes, zekeringwaarden en exacte productkeuzes
  zijn nog vrij invulbaar zonder architecturale impact.

Als hieraan is voldaan, is de target geschikt voor merge naar `main`.

---

## Vastleggen van de bestaande installatie (as‑is)

De bestaande installatie wordt vastgelegd als **snapshot** uitsluitend om:

- verschillen met de target zichtbaar te maken,
- een migratiepad te bepalen,
- en latere troubleshooting mogelijk te maken.

Een as‑is snapshot wordt **alleen gemaakt nadat**
de target‑architectuur in `main` is vastgelegd.

### Normatieve werkwijze as‑is snapshot

1. Start vanuit `main`
2. Maak `current/as-is-YYYY-MM`
3. Pas schema’s aan tot ze de **feitelijke werkelijkheid** beschrijven
4. Commit dit als waarheidssnapshot
5. De branch wordt daarna niet verder ontwikkeld

As‑is snapshots hoeven niet mooi te zijn;
ze moeten correct zijn.

---

## Relatie tussen target en as‑is

- De target beschrijft **waar het systeem naartoe gaat**.
- As‑is beschrijft **hoe het systeem er werkelijk uitziet**.

Het migratiepad wordt afgeleid uit de verschillen tussen beide,
niet door de target aan te passen aan de bestaande situatie.

---

## Gebruik van ADR’s

- Elke blijvende architecturale keuze hoort in een ADR.
- Schema’s volgen ADR’s, niet andersom.
- Als een schema‑wijziging niet door een ADR wordt gedragen,
  ontbreekt er óf een ADR, óf de wijziging is onjuist.

Het overzicht en leesadvies van ADR’s staat in `docs/adr/ADR-INDEX.md`.

---

## Normatieve stelregel

> Ontwerp beschrijft intentie.  
> As‑is beschrijft werkelijkheid.  
> ADR’s beschrijven besluiten.  
> Git bewaart alles.
