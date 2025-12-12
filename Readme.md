# Bottle Filling Line – PLC Project

This project simulates a 500 ml Coca-Cola bottle filling line. The main idea is that a bottle is transported on a conveyor, detected by a sensor, filled according to the calculated filling time, and then closed before leaving the station. 

## Project Overview

The simulated process works as follows:
1. A conveyor transports empty bottles.
2. When the sensor detects a stable bottle, the conveyor stops.
3. The production task fills the bottle based on a calculated filling time.
4. After filling, the bottle is closed
5. The conveyor removes the finished bottle and waits for the next one.

## Components

### 1. ConveyorTask (PROGRAM)
This part has to main roles, it handles the conveyor movement and bottle detection:
- Detects when a bottle arrives.
- Stops the conveyor.
- Signals that the bottle is ready to be filled.
- Moves the bottle away after filling.

### 2. ProductionTask (PROGRAM)
This part controls the filling and closing process:
- Calculates the filling time.
- Opens the fill valve
- When the bottle is Filled the cap is closed
- Marks the bottle as finished.

### 3. Global Variable List (GVL)
Here is where the main commands are named
- Sensor and actuator states
- Process parameters (bottle volume, filling rate)
- Synchronization signals (BottleReadyForFill, BottleFilled)

### 4. CalculateFillTime_ms (FUNCTION)
Here with a number that makes sense for the 500 ml bottle it measures the filling time in milliseconds based on:
- Bottle volume  
- Flow rate  

The function returns a value between 0 and 60000 ms.

## Tasks

The project uses two independent real-time tasks:
- ConveyorTask_Cycle: runs the conveyor logic  
- ProductionTask_Cycle: runs the filling and capping logic

Each task has its own cycle time and they operate in parallel.

## Documentation (PlantUML)

The repository includes 4 PlantUML diagrams explaining the main process
- State diagram – ConveyorTask  
- State diagram – ProductionTask  
- Sequence diagram – communication between both tasks  
- Sequence diagram – function call from ProductionTask  

## Main Conclusion
It has been a complete project, as we have to first think of a process that was not to complex, then create a code that could virtually replicate what we were triying to tramsit. Also, the diagrams were the most difficult part in my opinion, as we had to deliver something understandable for everyone who looks at the project, Otherwise, the idea and concept would make little sense.