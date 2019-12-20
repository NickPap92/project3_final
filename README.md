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

#### Pdynamic = aC(V^2)f

where **a** is the switching activity factor that relates to how many transitions occur between digital states (i.e., 0 to 1 or vice versa) in the processor, **C** is the total capacitance load, **V** is the supply voltage, and **f** is the clock frequency of the processor.

&nbsp;

There is a strong relationship between the CPU utilization and total power consumption. The idea behind the proposed model is that the power consumption grows linearly with the growth of the CPU utilization from the value of the power consumption in the idle state up to the power consumed when the CPU is fully utilized. This relationship can be expressed as in:

#### P(u) = Pidle+(Pbusy − Pidle)×u

where **P** is the estimated power consumption, **Pidle** is the power consumption by an idle server, **Pbusy** is the power consumed by the server when it is fully utilized, and **u** is the current CPU utilization. 

By this we can see that there is a direct relationship between time needed to execute a program and power consumption. If we assume that a program is set to run as soon as the system fires up, and that program is taking a considerable amount of time to run (for instance Prime95 small ftt 24hr stress test run), we can calculate the total power consumption as:

&nbsp;
Assuming **Pidle** is close to zero and **u** is 100% for the first 24hrs:
#### P(u) = (Pbusy) = P(uMax)

&nbsp;

Let's see how different programs affect **Dynamic power** and **Static power(Leakage)**.

**Dynamic power** is affected by **a**, **C**, **V** and **f**. 

- Switching activity factor [**a**]

    It depends on both the logic function being performed and the statistical properties of
    the primary inputs. the expected value of the number of gate output transitions per global clock cycle or equivalently the average number of gate output transitions per clock cycle.
