# To do list

## Algemeen

- **DONE** Verwijder .kicad_pcb. Die is niet relevant voor de architectuur want is printplaat layout.
- **DONE** Maak 2 interface componenten:
  - **DONE** IF_GENERIC met 1 passieve pin, voor signaal verbindingen (NMEA2000, VE_CAN, etc).
  - **DONE** IF_POWER met 1 power input pin, voor power verbindingen (aders in AC en DC).
- Kleurgebruik:
  - **DONE** Geen kleur gebruiken voor subsheets
  - Kleur gebruiken voor componenten: RGB ongeveer 230,230,230 of KiCad “background fill” zeer licht (CoPilot aanrader lichtgrijs, 5–15% dekking, geen pure kleuren (rood/blauw/groen))

## 00

- **DONE** RF signaal als netlabel op 00 zetten
- **DONE** gebruik op 00 AC_IN en label ook de draden conform. Gebruik nergens puur AC, maar maak duidelijk wat de herkomst is.
- **DONE** eerst 00 tekenen, dan hoofddomeinen, dan pas verdere detaillering. Niet tussendoor dingen toevoegen op 00.
- **DONE** 00 moet logisch compleet zijn, ook al is er nog geen detailengineering. Er mogen geen open vragen zijn die alleen door herstructurering van 00 kunnen worden opgelost.
- **DONE** 00 moet stabiel zijn voordat verdere detaillering plaatsvindt. Detaillering mag geen wijzigingen aan 00 vereisen.
- **DONE** walstroomaansluiting: als male connector met alle pinnen Power Input.

## Domeinbladen

- gebruik een interface component die ik aansluit op de hierarchische poort, zodat ERC kan controleren of er een verbinding is. Deze component zal vanzelf niet meer nodig zijn nadat het domeinblad is uitgewerkt, maar is nu nodig om de verbindingen te kunnen modelleren en controleren.
- **DONE** op 10 de power flag voor walstroomaansluiting, zodat ERC kan controleren of er een verbinding is.
