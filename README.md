# Traffic-Light-FSM
ECE2029 Final Project (WPI)

Introduction
Traffic Signals are a crucial part of urban traffic management, ensuring a safe and organized way for flow of traffic and pedestrians through different intersections. The main goal of the project we are making is to design a 2-way Traffic light system using FSM in Verilog. The design includes all the required things like: 
•	North, South Traffic lights with Green, Yellow and Red Lights
•	Pedestrian Crossing functionality using button
•	Timers controlling durations of all the things listed above.
This project demonstrates how FSM can be used in real life scenarios and also can be extended to the 4 Way Traffic system.

Problem Statement:
Managing an intersection in the urban area, with high traffic and pedestrian walking around. There were stop signs on each side of the road, but they were ineffective causing crashes between cars and pedestrians. 
We aim to solve the problem by implementing the following:
1)	Design system that will manage traffic effectively and safely.
2)	Control duration of green, yellow, and red signals to better improve flow of traffic.
3)	Improve safety precautions for pedestrian crosswalks.
Goal: The system works correctly, is safe for traffic and pedestrians, can be expanded later, and can eventually be turned into a real, working traffic light controller.

Proposed Solution:
The FSM consists of 8 states, in which each represents traffic or pedestrian conditions.
State Name                                                                         Description
S0_S_Green	South traffic light Green, North Red
S1_S_Yellow	South traffic light Yellow, North Red
S2_ALL_RED_1	All Traffic lights Red
S3_N_Green	North traffic light Green, South Red
S4_N_Yellow	North traffic light Yellow, South Red
S5_ALL_RED_2	All Traffic lights Red
S6_PED_ALL_RED	All Traffic lights Red, Pedestrians walk
S7 PED_NO_WALK	The next green light will turn on, Pedestrians not allowed to walk.

State Transitions:
1)	Each green and yellow signal is timed
2)	There is an all-red signal after every cycle (Green, Yellow) to avoid accidents.
3)	After the Pedestrian button is pressed, there is an application of S6_PED_ALL_RED where the next cycle of traffic becomes all red.
4)	After Pedestrian button duration ends, the traffic resumes where it left before normal.
Assumptions:
1)	If the South signal is green, the vehicles go left, right and straight. If the North signal is green, the vehicles go left, right and straight. 
2)	Both cannot be green at the same time.
3)	Timings are:
•	Green: 20 seconds
•	Yellow: 6 seconds
•	All-Red: 2 seconds
•	Pedestrian walk: 8 seconds
4)	Pedestrian requests are handled only at all red signals and can be requested from any side.
 

Verilog Implementation:
FSM is used in Verilog for the traffic light controller.
Inputs:
•	clk – System clock
•	reset – to initialize FSM
•	ped_button: pedestrian request button
Outputs:
•	R_S, Y_S, G_S: South traffic lights (Red, Yellow, Green)
•	R_N, Y_N, G_N: North traffic lights (Red, Yellow, Green)
•	
Timer implementation:
•	A 16-bit timer register counts the duration of each state.
•	On a state change, the timer is reset to 0.
•	While in the same state, the timer increases with each clock cycle.
•	When the timer reaches the already defined duration for the current state, the FSM continues to the next state.
Output logic:
Outputs are assigned based on the current state. 
Example:
S0_S_Green: Southern Traffic light is green (Value = 1), North is red (0). Pedestrian walk is off (0).


Simulation Results:
Simulation Setup
•	Clock period: 10 ns
•	Reset: high for the first 20 ns (Value = 1)
•	Pedestrian button: Tested by pressing at different times during traffic cycles
•	Outputs observed: R_S, Y_S, G_S, R_N, Y_N, G_N

Test Cases Considered:
1)	Normal Traffic Cycle 
FSM cycles through:
S0_S_GREEN → S1_S_YELLOW → S2_ALL_RED_1 → S3_N_GREEN → S4_N_YELLOW → S5_ALL_RED_2 → S0_S_GREEN
     

2)	Pedestrian Presses Button during Green/Yellow:
The FSM allows pedestrians button to be requested at any time, and will always give priority by the Pedestrian walk signal turning on for the Next All Red.

3)	Edge Cases: Pedestrian button pressed multiple times consequently
FSM handles this problem by allowing just one Pedestrian button cycle request.

Observed Waveform: 
 
  
Analysis of Results
1)	The FSM successfully cycles through all states with correct timings.
2)	Pedestrian requests are handled safely without conflicting with vehicle traffic.
3)	All expected output patterns match the FSM design table.

Conclusion: 
I successfully created and implemented a fully functional working 2-way traffic light system with Pedestrian crosswalks, using FSM in Verilog. For this project we have a total of 8 states ,12 gates and 9 I/O. 

 Simulation confirms correct behavior of all the modes:
1)	Cycle of North and South traffic light signals
2)	Proper timings
3)	Handling of pedestrian button
From this project, we learned FSM structures like state encoding, next-state logic, and output logic. We also learned how to implement these FSM structures in real life scenarios. 

Future Work
1)	Can be extended to handle a 4-way traffic light signals by adding more cases
2)	Could create a LED Pedestrian Walk or Stop. When the pedestrian request button is 1, this LED sign displays a green Walk sign, else it shows a Red Stop sign. 
3)	Can improve the 2-way traffic system to be more efficient.


