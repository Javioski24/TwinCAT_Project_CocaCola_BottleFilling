@startuml TasksCommunication_Student

title Task Communication Flow (Conveyor <-> Production)

participant Conveyor
participant "GVL\n(Shared Variables)" as GVL
participant Production

== BOTTLE READY ==
Conveyor -> GVL : SET gBottleReadyForFill
Conveyor -> Conveyor : Conveyor Stop

== FILLING START ==
Production -> GVL : READ gBottleReadyForFill
Production -> Production : Calculate Time & Start FillTON\nOpen Fill Valve

== FILLING END / BOTTLE CAP BEGINS ==
Production -> Production : FillTON.Q = TRUE
Production -> GVL : SET gBottleFilled
Production -> Production : Start CapTON

== CAP CLOSED ==
Production -> Production : CapTON.Q = TRUE\nCapper OFF (DONE)

== EVACUATION ==
Conveyor -> GVL : READ gBottleFilled
Conveyor -> Conveyor : Start Conveyor (Evacuate)

== CYCLE RESET ==
Conveyor -> GVL : RESET gBottleFilled
Production -> GVL : READ gBottleFilled
Production -> Production : Return to IDLE (Ready for next)

@enduml
