```Plantuml
@startuml 

title Diagrama de Estados - ConveyorTask

[*] --> RUNNING

state RUNNING
note right of RUNNING
  State = 0
  gConveyorStateStr := 'RUNNING'
  gActuator_ConveyorRun := TRUE
end note

state STOPPED
note left of STOPPED
  State = 1
  gConveyorStateStr := 'STOPPED'
  gActuator_ConveyorRun := FALSE
end note

state EVACUATE
note right of EVACUATE
  State = 2
  gConveyorStateStr := 'EVACUATE'
  gActuator_ConveyorRun := TRUE
end note

'Transitions'

RUNNING --> STOPPED : DebounceTON.Q (Firm Bottle Detected) / gBottleReadyForFill := TRUE
STOPPED --> EVACUATE : gBottleFilled = TRUE (Filling up completed) / gBottleReadyForFill := FALSE
EVACUATE --> RUNNING : (NOT gSensor_BottleDetected) AND EvacuateTON.Q (Evacuation Ends) / gBottleFilled := FALSE

@enduml
```