sequenceDiagram
title Function: CalculateFillTime_ms

participant ProductionTask
participant "CalculateFillTime_ms()" as Func

%% Check Condition
ProductionTask ->> ProductionTask: gBottleReadyForFill = TRUE
Note right of ProductionTask: Prerequisite from ConveyorTask

%% Function Call
ProductionTask ->> Func: CalculateFillTime_ms(vol_l, rate_Ls)
activate Func

Func ->> Func: Run Logic
Note right of Func:
1. Validate Input (rate_Ls <= 0 → return 0)
2. Calculate t_ms = (Volume / Rate) * 1000
3. Clamp t_ms between 0 ms and 60000 ms

Func -->> ProductionTask: return tFill_ms (DINT)
deactivate Func

%% Action
ProductionTask ->> ProductionTask: Start FillTON(PT := tFill_ms)\nOpen FillValve
