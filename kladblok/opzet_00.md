# Opzet voor sheet 00

Alle pinnen met dezelfde naam zijn verbonden op 00

## 00

Items op dit sheet buiten subsheets en connecties:

- walstroom aansluiting als connector met AC_IN_L, AC_IN_N, PE. Alledrie Power input, bundelen in bus AC_IN aangesloten op die pin op 10
- radiosignaal RF als netwerk, aangesloten op RF pin van 20.
- N2K - VE.can bridge met 2 pinnen: N2K, VE_CAN. Aangesloten op die netwerken.

## 10 AC

- AC_IN passief
- DC_POS_HOUSE, DC_NEG_HOUSE power input
- DC_POS_CHARGER, DC_NEG_CHARGER power output
- VE_CAN passief

## 20 DC

- DC_POS_HOUSE, DC_NEG_HOUSE power output
- DC_POS_START, DC_NEG_START power output
- DC_POS_CHARGER, DC_NEG_CHARGER power input
- DC_POS_ALTN, DC_NEG_ALTN power input
- VE_CAN passief
- N2K passief
- RF passief

## 30 Engine

- DC_POS_START, DC_NEG_START power input
- DC_POS_ALTN, DC_NEG_ALTN power output
- N2K passief
- SIG_ENG_START input

## 40 Sensors

- N2K passief

## 50 Displays

- N2K passief
- SIG_ENG_START output

## 90 References

- alle DC_NEG_* pinnen passief, voor zover verbonden via engine case. Binnen 90 heb ik dan een component ENGINE_CASE met meerdere pinnen DC_NEG_HOUSE, DC_NEG_START etc.
