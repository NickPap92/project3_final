# Architecture Lab, Project 3

## Detailed Report

## Step 1. 

&nbsp;

### 1.

&nbsp;

Modern processors are built over complementary metal-oxide semiconductor (CMOS) technology. The main power consumption in CMOS circuits comprises two forms of power, dynamic power consumption (Pdynamic) and static power consumption (Pstatic). The static power consumption, also known as idle power or leakage, is the dominant source of power consumption in circuits, persisting whether a computer is active or idle. Leakage power consumption is caused by parasitic current that flows through transistors, due to their construction, even when the transistor is switched off. In addition to consuming static power, computer components also consume dynamic power due to circuit activity such as the changes of inputs in an adder or values in a register. 

&nbsp;
Total power can be determined by this equation:

#### P = Pstatic + Pdynamic

&nbsp;
Dynamic power can be approximately determined by:

#### Pdynamic = aC(V^2)f,

where a is the switching activity factor that relates to how many transitions occur between digital states (i.e., 0 to 1 or vice versa) in the processor, C is the total capacitance load, V is the supply voltage, and f is the clock frequency of the processor.
