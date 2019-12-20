# Architecture Lab, Project 3

## Detailed Report

## Step 1. 

&nbsp;

### 1.

&nbsp;
Modern processors are built over complementary metal-oxide semiconductor (CMOS) technology. The main power consumption in CMOS circuits comprises two forms of power, dynamic power consumption (Pdynamic) and static power consumption (Pstatic). **The static power consumption, also known as idle power or leakage, is the dominant source of power consumption in circuits, persisting whether a computer is active or idle**. Leakage power consumption is caused by parasitic current that flows through transistors, due to their construction, even when the transistor is switched off. In addition to consuming static power, computer components also consume dynamic power due to circuit activity such as the changes of inputs in an adder or values in a register. 

&nbsp;
Total power can be determined by this equation:

#### P = Pstatic + Pdynamic

&nbsp;
Dynamic power can be approximately determined by:

#### Pdynamic = aC(V^2)f

where **a** is the switching activity factor that relates to how many transitions occur between digital states (i.e., 0 to 1 or vice versa) in the processor, **C** is the total capacitance load, **V** is the supply voltage, and **f** is the clock frequency of the processor.

&nbsp;

There is a strong relationship between the CPU utilization and total power consumption. The idea behind the proposed model is that the power consumption grows linearly with the growth of the CPU utilization from the value of the power consumption in the idle state up to the power consumed when the CPU is fully utilized. This relationship can be expressed as in:

#### P(u) = Pidle+(Pbusy − Pidle)×u

where **P** is the estimated power consumption, **Pidle** is the power consumption at idle, **Pbusy** is the power consumed by the server when it is fully utilized, and **u** is the current CPU utilization. 

By this we can see that there is a direct relationship between time needed to execute a program and power consumption. Given that **Pidle** is static, the higher the **Pbusy** is, the higher the total power consumption.

&nbsp;

&nbsp;
[Dynamic Power Consumption](https://www.sciencedirect.com/topics/computer-science/dynamic-power-consumption)

Let's see how different programs affect **Dynamic power** and **Static power(Leakage)**.

&nbsp;
**Dynamic power** is affected by **a**, **C**, **V** and **f**. 

- Switching activity factor [**a**]

    It depends on both the logic function being performed and the statistical properties of
    the primary inputs. It is defined as the expected value of the number of gate output transitions per global clock cycle     or equivalently the average number of gate output transitions per clock cycle.

The closer a program's CPI to 1.0 is, the more instructions per clock it executes, the more gate output transitions happen and therefore **a** increases.

[Estimation of average switching activity](https://www.researchgate.net/publication/220400097_Estimation_of_average_switching_activity_in_combinational_logic_circuits_using_symbolic_simulation)

&nbsp;

- Capacitance load [**C**]

    It is the amount of capacitance measured or computed across the crystal terminals on the PCB. 

    Every mos transistor as a switch in the circuit has an input CGS capacitance and a an on-resistance. So, if we build a circuit using this transistor it will react on the abrupt input voltage changes by a slowing the change of the output voltage from the high to low and from the low to high. Which means that the output voltage will not change instantly but will take time to charge and discharge the output load capacitor. Increasing the input pulse rate by increasing its frequency will lead to shrink the steady state time of the pulses which will ultimately be zero and the output waveform will appear triangular. This will be the maximum input possible bit rate.

Therefore, if our CPU is running on a fixed voltage and frequency, **C** remains static. In the case of dynamic frequency, capacitane load will slowly change according to alterations in frequency, which depend on temperature, power and current limits.

[What is load capacitance](https://www.quora.com/What-is-load-capacitance)

[Pierce oscillator](https://en.wikipedia.org/wiki/Pierce_oscillator#Load_capacitance)

[Load Capacitance](https://www.sciencedirect.com/topics/engineering/load-capacitance)

[Resonance](https://en.wikipedia.org/wiki/Resonance)

[Do frequency changes affect on load capacitance of VLSI circuits](https://www.researchgate.net/post/Do_frequency_changes_affect_on_load_capacitance_of_VLSI_circuits)

&nbsp;

- Supply voltage [**V**]

    The voltage supplied to the CPU. Can be fixed or dynamic. Greatly affects Dynamic power as we calculate the **V^2** value.

&nbsp;

- CPU frequency [**f**]

    The frequency the CPU is running at. Can be fixed or dynamic.

&nbsp;
**Static power(Leakage)** is present whether the computer is active or idle. It is due to leakage current and depends primarily on the manufacturing process and technology with which the transistors are made. It does not depend on the frequency of operation of the flip-flops.

[Static power](https://www.sciencedirect.com/topics/computer-science/static-power)

&nbsp;

&nbsp;

### 2.

&nbsp;
In order to determine which CPU is more energy efficient, we need to examine different cases of the problem.

- Case 1: 
