# Structuur bladen in KiCad

- 00_TopLevel.sch (integratie + expliciete koppelingen)
- 10_Power_AC.sch (facade; 1 AC-groep, losse lader)
  - 11_Shore_Inlet_And_Protection.sch
  - 12_AC_Loads.sch (stopcontacten/boiler)
  - 13_Battery_Charger.sch (AC→DC house)
- 20_Power_DC.sch (facade; house/start rails)
  - 21_Batteries_House.sch
  - 22_Batteries_Start.sch
  - 23_Charging.sch (laadrelais/DC-DC/MPPT; dynamo staat op Engine Core)
  - 24_DC_Distribution.sch (met 24.x subbladen; incl. 24_Comms)
- 30_Engine.sch (facade; bevat 31/32/33)
  - 31_Engine_Core.sch
  - 32_Engine_Sensors.sch
- 40_UserInteraction.sch (facade; bevat 41/42)
  - 41_SystemIndication.sch (wat ziet de mens)
  - 42_UserControl.sch (wat doet de mens, alleen als er een signaal wordt gestuurd, niet als schakelaar werkt door stroom te onderbreken) -> SIG_ENG_START input wordt hier gemaakt, en SIG_AP (signaal autopilot)
- 50_Sensors.sch (facade; systeem-sensorgeving, beginpunten van data)
  - 51_Nav_Sensors.sch (wind/log/diepte/heading/GPS)
  - 52_Other_Sensors.sch (optioneel)
- 60_System_Infrastructure_(Physical_&_Protocol).sch (facade; verduidelijking/implementatie)
  - 61_RF_VHF.sch (detailblad; antenne/coax/mastvoet)
  - 62_N2K.sch (detailblad; backbone/terminators/T-stukken)
  - 63_AnalogGateways.sch (optioneel)
  - 64_Mast_Wiring.sch (optioneel; looms/bussen door de mast)
- 90_References.sch (betekenis/grondslagen)

Toelichting 60-laag (System Infrastructure)

- De 60-laag beschrijft de fysieke en protocolmatige realisatie van signalen/netwerken die elders functioneel worden gebruikt.
- Subbladen onder 60 introduceren geen nieuwe functionaliteit; ze maken impliciete aannames expliciet (kabelroutes, looms, backbone-structuur).
- Zonder 60 blijft het systeem functioneel correct; met 60 wordt het systeem begrijpelijker en onderhoudbaar.
