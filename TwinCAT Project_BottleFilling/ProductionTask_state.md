```Plantuml
@startuml 

title ProductionTask - State Diagram

[*] --> IDLE

state IDLE
note right of IDLE
  State = 0
  gProductionStateStr := 'IDLE'
  FillValve = OFF
  Capper    = OFF
  Waiting for gBottleReadyForFill
end note

state FILLING
note left of FILLING
  State = 1
  gProductionStateStr := 'FILLING'
  gActuator_FillValve := TRUE
  FillTON running (PT = tFill_ms)
end note

state CAPPING
note left of CAPPING
  State = 2
  gProductionStateStr := 'CAPPING'
  gActuator_Capper := TRUE
  CapTON running (PT = 400ms)
end note

state DONE
note right of DONE
  State = 3
  gProductionStateStr := 'DONE'
  Waiting for evacuation of bottle
  (gBottleFilled = FALSE)
end note

IDLE --> FILLING : gBottleReadyForFill == TRUE\nCalculateFillTime_ms\nStart FillTON
FILLING --> CAPPING : FillTON.Q == TRUE\nFillValve := FALSE\nCapTON start\n gBottleFilled := TRUE
CAPPING --> DONE : CapTON.Q == TRUE\nCapper := FALSE
DONE --> IDLE : gBottleFilled == FALSE

@enduml
```