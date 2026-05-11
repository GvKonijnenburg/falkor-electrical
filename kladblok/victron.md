# Victron setup

## GX

Aansluitingen:

- VE_CAN passief
- VE_CAN passief
- VE_DIRECT passief
- VE_DIRECT passief
- HDMI passief
- USB passief

## GX Touch

Aansluitingen:

- HDMI / USB passief aangesloten op bus {HDMI USB} met GX

## DC-DC lader

Aansluitingen:

- VE_DIRECT passief aangesloten op GX
- DC_POS_IN power input aangesloten op start accu
- DC_POS_OUT power output aangesloten op Lynx?
- GND aangesloten op massa

## Lynx BMS

- VE_CAN passief aangesloten op GX
- BMS_MALE passief aangesloten op huisaccu 1
- BMS_FEMALE passief aangesloten op huisaccu 2

## Lynx Distributor

Pinnen

- POS_RAIL_IN     (DC_POS_HOUSE)
- POS_RAIL_OUT    (DC_POS_HOUSE)
- NEG_RAIL_IN     (DC_NEG_HOUSE)
- NEG_RAIL_OUT    (DC_NEG_HOUSE)
- DATA_RJ10_L
- DATA_RJ10_R
- POS_FUSED_1
- POS_FUSED_2
- POS_FUSED_3
- POS_FUSED_4
- NEG_LOAD

Aansluitingen:

- DC_POS_HOUSE power input op huis accu
- DC_NEG_HOUSE power input op huis accu
- DC_POS_INVERTER power output naar inverter
- DC_POS_ESSENTIAL power output naar essentiële verbruikers
- DC_POS_COMFORT power output naar niet-essentiële verbruikers
- DC_NEG_HOUSE power output naar verbruikers en inverter
