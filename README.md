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
In order to determine which CPU is more energy efficient, we need to examine different cases of the problem. We will assume that the processors are not entirely in an idle state, as this would make it obvious the 5W CPU is more efficient. We also assume that the processors are running a certain workload, as in video decoding or 3D rendering.

- Case 1: System starts up, workload is executed, task is finished and CPU idles until battery drains out.

- Case 2: System starts up, workload is executed, task is finished and system shuts down.

- Case 3: Battery drains out before workload is completed.

&nbsp;

Let's take the example of a Penryn CPU built on 45nm node. This one has a runtime dynamic o 36.1433W, which is close to the theoretical 40W CPU we are examining. Runtime consumption refers to the consumption while the CPU is executing machine code.

Our competitor will be an ARM\_A9\_2GHz\_withIOC, built on 40nm node which is slightly more refined than the Penryn and thus having a slight edge on the power consumption on top of being a low power budget component. The runtime dynamic of this CPU is 5.57062W.

Both CPUs will have a statik leakage being idle or not. The ARM processor has a subthreshold leakage of 0.0559042W, whereas Penryn's is 8.67012W. Penryn is built on an architecture that can take advantage of power gating, leading to 4.25769W of subthreshold leakage with power gating. This technology makes it possible for the CPU to completely block all current passing through a gate when it's closed, when normally even if a gate is closed it is run by some current and that helps with power consumption. 

Given that Penryn is on a high power budget envelope, it incorporates way more instructions per cycle. As we saw, higher IPC ( or lower CPI ) has a detrimental effect on the duration of a code execution.

With these in mind let's examine all 3 of the cases.

&nbsp;

#### Case 1

If the executed code takes a considerable longer amount of time to be executed, it means that after it is done executing on the Penryn, the CPU will idle and consume 4.25769W in the subthreshold leakage with power gating stage, whereas on the ARM it might still be executing the code consuming 5.57062W. This can give an edge on the Penryn CPU as it will be consuming less wattage than a still-executing 5W ARM CPU.

&nbsp;

#### Case 2

In this case, similarly to the first one, Penryn will finish executing the code and system powers off, saving battery life by not consuming any leakage power which is a substantial amount.

&nbsp;

#### Case 3

In this case battery efficiency does not really matter as none of the CPUs achieved desired goal.

&nbsp;

&nbsp;

By running commands like "./mcpat \-infile ProcessorDescriptionFiles/Xeon.xml \-print\_level 5", Mcpat can give us details about total leakage, runtime dynamic, peak power consumption as well as consumption about individual components of the CPU such as L1 and L2. This is a short benchmark of the CPU but we would also need to know the duration of it, the CPU percent load and the instruction sets used to determine the power efficiency of the CPU.

Sources:

[Runtime](https://en.wikipedia.org/wiki/Runtime_(program_lifecycle_phase))

[Is the ARM processor more energy efficient than Intel?](https://www.researchgate.net/post/Why_is_the_ARM_processor_more_energy_efficient_than_Intel)

[Does a x86 CPU run faster than an ARM equivalent counterpart?](https://www.quora.com/Given-the-same-clock-frequency-does-a-x86-CPU-run-faster-than-an-ARM-equivalent-counterpart)

[CPU utilization & power consumption](https://www.quora.com/Does-a-weak-CPU-on-100-or-a-strong-CPU-on-50-consume-more-electricity)

&nbsp;

&nbsp;
### 3.

&nbsp;

