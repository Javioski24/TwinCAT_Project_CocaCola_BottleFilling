```Mermaid
@startuml 
title Function: CalculateFillTime_ms 

participant ProductionTask
participant "CalculateFillTime_ms()" as Func

== Check Condition ==
ProductionTask -> ProductionTask : gBottleReadyForFill = TRUE
note right: Prerequisite from ConveyorTask

== Function Call ==
ProductionTask -> Func : CalculateFillTime_ms(vol_l, rate_Ls)
activate Func

Func -> Func : Run Logic
note right
  // Logic Steps:
  1. Validate Input (IF rate_Ls <= 0 THEN return 0)
  2. Calculate t_ms = (Volume / Rate) * 1000
  3. Clamp t_ms between 0 ms and 60000 ms
end note

Func --> ProductionTask : return tFill_ms (DINT)
deactivate Func

== Action ==
ProductionTask -> ProductionTask : Start FillTON(PT := tFill_ms)\nOpen FillValve

@enduml
```