# ADR-013 — Afbakening van 42_SwitchPanel

**Status:** Geaccepteerd  
**Datum:** 2026-05-07

## Context en probleemstelling

In `42_SwitchPanel` wordt bediening gemodelleerd die menselijke intentie het systeem in brengt. Zonder afbakeningsregel ontstaat het risico dat interne apparaatbediening (bijv. een knop op een koelkast) onbedoeld als los systeemobject wordt gemodelleerd, wat tot ruis en inconsistentie leidt.

## Beslissingscriteria

- 42 blijft semantisch scherp (bediening/intent, geen apparaat-interne details).
- Modellering ondersteunt troubleshooting, service en vervanging.
- Geen dubbel modelleren van apparaat-interne functies.

## Overwogen opties

- **Optie A — Alle bedieningen in 42 modelleren**  
  Elke fysieke of logische bediening, inclusief stroomonderbrekende
  schakelaars en circuitbreakers, wordt als bedieningsobject gemodelleerd in 42.

- **Optie B — Alle zelfstandig vervangbare bedieningen in 42 modelleren**  
  Bedieningen worden in 42 geplaatst als zij los bestaan en afzonderlijk
  te servicen of te vervangen zijn, ongeacht hun rol in het energiepad.

- **Optie C — Bedieningen modelleren op basis van functionele rol**  
  Bedieningen die systeemgedrag aansturen (commando’s, setpoints, modes)
  worden gemodelleerd in 42; fysieke vermogensschakeling blijft in het
  energiedomein.

- **Optie D — Alleen intentie‑gedreven bedieningen in 42 modelleren (gekozen)**  
  Alleen bedieningen die **menselijke intentie vertalen naar een logisch
  commando** krijgen een plek in 42. Fysieke stroomonderbrekende schakelaars,
  vermogensschakelaars en circuitbreakers maken expliciet deel uit van het
  energiepad en worden gemodelleerd in het toepasselijke energiedomein.

## Besluit

Gekozen is voor **Optie D — Alleen intentie‑gedreven bedieningen in 42 modelleren**.

42_SwitchPanel wordt daarmee uitsluitend gebruikt voor bedieningselementen die menselijke intentie omzetten in logische commando’s of instellingen. Bedieningen die fysiek onderdeel zijn van het energiepad, zoals stroomonderbrekende schakelaars en circuitbreakers, worden beschouwd als vermogenscomponenten en gemodelleerd in de relevante energiedomeinen.

## Gevolgen

### Positief

- 42 blijft schoon en consistent.
- Troubleshooting en vervangbaarheid worden expliciet.

### Negatief

- Sommige interne bedieningen blijven impliciet (bewust) en worden niet apart getekend.

## Toepassing en bevestiging

- Bij elk bedieningsdeel wordt beoordeeld of het een stuursignaal levert en zelfstandig kan worden onderhouden/vervangen.
- Alleen dan krijgt het een plek in 42; anders blijft het onderdeel van het apparaat in het betreffende domein.

### Notities / vervolg

Voorbeelden

- losse autopilot-bedienkop → 42.
- knop in koelkastdeur → niet 42, onlosmakelijk deel van apparaat.
- lichtschakelaar die stroom onderbreekt → niet 42, maar in energiedomein.
