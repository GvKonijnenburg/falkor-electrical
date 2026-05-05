# Working notes – Falkor Electrical (praktisch)

Dit document is een **praktische instap- en sessiehandleiding**.  
Het helpt om na een pauze snel weer correct en consistent te werken.

Dit document is **niet normatief**.  
Regels en beslismomenten staan in `WORKFLOW.md` en in de ADR’s.

---

## Is deze repository opnieuw geinstalleerd?

- Ja -> doe het volgende:
  - kopieer tools\precommit naar .git\hooks\pre-commit
  - in git bash: ```chmod +x .git/hooks/pre-commit```

Dit zorgt ervoor dat alles in de folder kladblok alleen in work\branches kan bestaan.

## Wat doe ik bij een nieuwe werksessie?

### 1. Context herstellen

- Bepaal het doel van deze sessie:
  - structuur verbeteren?
  - 00_TopLevel toetsen?
  - één domein uitwerken?
  - bestaande situatie inventariseren?

- Komt de actieve Git-branch overeen met het doel van deze sessie?
  (ontwerpwerk → feature branch; vastleggen werkelijkheid → current/as-is-*)

---

### 2. Afhankelijk van het doel

#### Target‑architectuur verder uitwerken

- Werk altijd in een **feature branch**
- Begin altijd bij **00_TopLevel**
- Werk daarna pas door naar:
  1. hoofddomeinen (10, 20, 50, …)
  2. subdomeinen (bijv. 24)
  3. infrastructuur (60)

#### Bestaande boot begrijpen

- Gebruik oud KiCad‑werk of fysieke inspectie als **inventarisatie**
- Niet als ontwerpbasis

---

## Praktische tekenregels (mentale checklist)

Stel bij elk element dat je tekent expliciet deze vragen:

- Is dit **architectuur** of **detailengineering**?
- Hoort dit bij:
  - systeemrelatie (00)?
  - functioneel domein?
  - distributie & beveiliging (24)?
  - fysieke uitleg (60)?
- Kan ik dit tekenen zonder een ADR te overtreden?

Bij twijfel:

> stop → ADR herlezen → dán pas tekenen

---

## Wanneer moet ik een ADR maken?

Maak een **nieuwe ADR** zodra je tijdens het werken één van de volgende vragen
met *“ja”* beantwoordt:

- Verandert dit de **architectuur**, niet alleen de uitwerking?
- Leg ik hiermee vast *hoe* het systeem werkt, niet alleen *wat* er hangt?
- Zou future‑me zich kunnen afvragen: *“waarom is dit zo gedaan?”*
- Is dit een keuze die ik later **niet automatisch zou terugdraaien**?
- Beperkt dit toekomstige ontwerpkeuzes of dwingt het een richting af?

Dan geldt: **eerst ADR, dán tekenen of aanpassen**.

---

### Wanneer géén ADR nodig is

Geen ADR nodig voor:

- detailengineering (kabeldiktes, zekeringwaarden, plaatsing);
- puur visuele schema‑aanpassingen;
- invulling van eerder vastgelegde besluiten;
- as‑is snapshots van de werkelijkheid.

Twijfelregel:

> Bij twijfel **wel** een ADR maken.  
> Een overbodige ADR is minder schadelijk dan een ontbrekende.

---

## Gebruik van bestaande (legacy) schema’s

Bestaande schema’s mogen dienen als:

- checklist van loads en sensoren
- geheugensteun ("dit zat er ook nog")

Ze worden **niet**:

- geïmporteerd
- opgeschoond
- of stap‑voor‑stap aangepast aan de nieuwe ADR’s

De target wordt **opnieuw opgebouwd**, niet gerefactord.

---

## Wanneer committen?

- Kleine denkstappen: meerdere commits in feature branch is prima
- Grote mijlpalen:
  - toets tegen de criteria in `WORKFLOW.md`
  - merge pas wanneer de target beslissingsrijp is

Commits beschrijven **gedachten en besluiten**, niet muisbewegingen.

---

## As‑is snapshots – praktische reminders

- Alleen maken als de target stabiel is
- Niets toevoegen wat er niet is
- Alles tonen wat er wél is
- Geen verbeteringen meenemen

Waarheid is belangrijker dan netheid.

---

## Als iets niet lekker voelt

Dat betekent meestal één van drie dingen:

1. Je zit op het verkeerde abstractieniveau
2. Er ontbreekt een ADR
3. Je probeert target en as‑is te mengen

Los dit eerst op voordat je verder tekent.
