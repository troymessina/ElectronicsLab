---
title: Chapter 2 - DC Resistor Circuits
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:resistors)=
# Overview
:::{hint} Learning Objectives
* Understand DC circuits and Ohm's Law.
* Understand the role of resistance in circuits.
* Understand methods of measuring current and voltage.
* Demonstrate the ability to draw, construct, and analyze resistor circuits.
:::

# Introduction

These experiments will be carried out with breadboards, multimeters, and DC power supplie. However, a useful virtual component to accompany the work on the lab bench is to use the PhET simulator below. Click on the "Lab" tab. 

:::{iframe} https://phet.colorado.edu/sims/html/circuit-construction-kit-dc/latest/circuit-construction-kit-dc_all.html
:label: chap:resistors:PhET
:width: 100%
:align: center
:placeholder: ../figures/ch2_resistors/PhETscreenshot.png
A PhET simulation to explore simple circuits.
:::

# Background
Ohm’s Law says 
```{math}
:label: eq:resistors:ohms
V = IR
```
or voltage equals the current times the resistance. $V$ is in Volts (Volts are Joules/Coulomb). $I$ is in amperes (or Coulomb per second), and $R$ is in Ohms (units you could work out from the others). These are SI units. Voltage, also called electric potential, is the source of energy pushing electrons through a typical circuit. Flowing charges, or current, is a result of the voltage pushing charges against electrical resistance. As voltage increases, the current should increase linearly for a particular resistance.
```{exercise}
:label: exercise:resistors:deliverable1
Set up the circuit in [](#fig:resistors:singleR) in the PhET simulation. Adjust the voltage of the battery from 0.5 V to 3 V. Explain what you observe is the response to increasing voltage in the circuit. Points to address are:
* What happens to the number of electrons flowing through the circuit per unit of time as voltage increases?
* Do electrons "pile up" at the resistor because the resistor has more resistance to flow than the wires? 
```

## Circuit Loop Rules
The word circuit comes from the idea that electronic circuits make loops. A circuit or electronic loop must conserve energy. This leads to two circuit rules.
1.	The sum of voltages around a loop are zero, e.g., energy per charge input from a battery equals energy per charge dissipated by a resistor.
2.	The current through a circuit or electronic loop is constant throughout the loop.

In [](#fig:resistors:singleR), on the left is a circuit shown as we might see in the lab with a battery and a resistor. On the right is the equivalent circuit diagram. We assume wires are ideal, with zero resistance. The circles with dashed lines are points where the circuit can be broken to add more elements such as a current meter.
```{figure} ../figures/ch2_resistors/singleR.png
:label: fig:resistors:singleR
:width: 80%
:align: center
:alt: Circuit showing a single resistor connected to a battery or power source. On the left is the PhET cartoon with a battery and 10 Ohm resistor. On the right is the circuit diagram.
Circuit showing a single resistor connected to a battery or power source. On the left is the PhET cartoon with a battery and 10 Ohm resistor. On the right is the circuit diagram.
```

```{exercise}
* Record what battery and resistor circuit diagrams look like. 
* Which side of the battery is +, and which side is -? You can determine this by the electron current flow.
* How is this polarity indicated in the circuit diagram on the right?
```
## Identifying Resistors

The resistors we will use have four or five colored bands on them. These bands quantify the resistance as shown in [](#fig:resistors:resistorBands).
```{figure} ../figures/ch2_resistors/resistorBands.jpg
:label: fig:resistors:resistorBands
:width: 100%
:align: center
:alt: Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
```
For example, a resistor with yellow, violet, red, and silver bands gives the numbers $4, 7, 2, \pm 10 \%$. This indicates the resistance is $47 \times 10^2=4700 \pm10 \%=4700 \pm470\Omega$.
 ```{exercise}
![Example resistor bands green, blue, orange, and gold](../figures/ch2_resistors/exampleBands.png)
* Calculate the resistance of the resistor shown in [](#fig:resistors:resistorBands) with green, blue, orange, and gold bands.
* Suppose this resistor is connected to a 3 Volt battery like the image of a circuit above. Using Ohm's Law in equation {eq}`eq:resistors:ohms`, what current will flow through the circuit?
```

## Measuring Voltage and Current

### 🔌 Voltage is Measured in Parallel

#### Why in parallel?
Voltage is the **potential difference between two points**. To measure that, you need to compare the electric potential at one point **relative to another**.

#### How?
- Place the **multimeter probes across** (in parallel with) the component.
- This allows the meter to measure the drop in electric potential **through** that component.

#### Example:
To measure the voltage across a resistor, you touch:
- One probe to the resistor's current input side.
- The other to the current output side.
- See [](#fig:resistors:elecmeasure)

💡 Think of it like checking the **pressure difference across a valve** in a water pipe.

---

### ⚡ Current is Measured in Series

#### Why in series?
Current is the **flow of electric charge** through a circuit. To measure it, the current must pass **through the multimeter** so it can count how much is flowing.

#### How?
- Break the circuit and insert the multimeter **in line** with the component (in series).
- This forces all the current flowing through that component to also go through the meter.

#### Example:
To measure the current through an LED, you'd:
- Disconnect one side of the LED.
- Connect the multimeter between the disconnected lead and where it was attached.

💡 This is like measuring **water flow by putting a meter in the pipe**—the water (or electrons) must pass through it.

---
```{figure} ../figures/ch2_resistors/volt_current_measure.jpg
:width: 80%
:align: center
:alt: A visual for how to measure voltage and current.
A visual for how to measure voltage and current.
```

### Quick Summary:

| Measurement | Connection Type | Why? |
|-------------|------------------|------|
| **Voltage** | Parallel          | Measures potential *difference* between two points |
| **Current** | Series            | Measures *flow* of charge through a path         |



# Experiment

## Part 1 – Single Resistor

Set up the circuit shown above with a single resistor in the simulator and on the lab bench. From the colored bands, determine the resistance and set the same resistance in the simulator. On the lab bench, you will use a power supply instead of a battery so that you can adjust the voltage. Apply the voltages as shown in the [](#tab:resistors:singleR) and measure the current flows for each applied voltage.
```{table} Applied voltages and measured currents.
:label: tab:resistors:singleR
:align: center
| Voltage (V) | Current (A) |
|:-----------:|:-----------:|
|      0.5    |             |
|      1.0    |             |
|      1.5    |             |
|      2.0    |             |
|      2.5    |             |
|      3.0    |             |
```
```{exercise}
:label: exercise:resistor:singleR
* Plot V vs I (y vs. x). Use the Python code below to add a linear fit to your data. What is the slope of your graph including uncertainty (We will go over graphing and fitting in Python.)? 
* How does your slope compare to the theoretical value of the resistor from its bands including uncertainty? Does the PhET simulation give the same results as your experiment? Explain.
```
```{code-cell} python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

#define a linear function
def line_fit (x, m, b):
	return m*x + b

#Define your data
V = np.array([0.5, 1.0, 1.5, 2.0, 2.5, 3.0])
V_unc = np.ones(6)*0.05 #adjust this to the appropriate uncertainty
I = np.array([1,2,3,4,5,6]) #enter your current values
I_unc = np.ones(6)*0.1 #adjust this to the appropriate uncertainty

#Do the linear fit
parms, cov = curve_fit(line_fit, I, V, sigma=V_unc, absolute_sigma=True)
print("slope =", parms[0], "+/-", np.sqrt(cov[0][0]))
print("intercept =", parms[1], "+/-", np.sqrt(cov[1][1]))

plt.errorbar(I, V, yerr=V_unc, fmt='ob') #plot the data
plt.plot(I, parms[0]*I+parms[1])
plt.xlabel('Current (A)')
plt.ylabel('Voltage (V)')
plt.show()
```
(sec:resistors:part2)=
## Part 2 – Series Resistors
Set up a "series" circuit with two resistors in series as shown in [](#fig:resistors:seriesR). From the colored bands, determine the resistances and set those same resistances and voltages in the PhET simulator.  Apply the input voltages as shown in [](#tab:resistors:singleR) and measure the currents at the locations indicated in [](#fig:resistors:seriesRImeas). Measure the voltage across each resistor (two voltage measurements).
```{figure} ../figures/ch2_resistors/seriesR.svg
:label: fig:resistors:seriesR
:width: 50%
:align: center
:alt: Circuit showing a two resistors in series connected to a battery or power source.
Circuit showing a two resistors in series connected to a battery or power source.
```
```{figure} ../figures/ch2_resistors/seriesR_Imeas.svg
:label: fig:resistors:seriesRImeas
:width: 50%
:align: center
:alt: Three locations identified for measuring current in the series circuit.
Three locations identified for measuring current in the series circuit.
```
```{exercise}
:label: exercise:resistor:seriesR
Using your results, show that $V=IR$ for each resistor within the uncertainty of the experiment.
```
## Part 3 - Parallel Resistors
Set up a "parallel" circuit with two resistors in parallel as shown in [](#fig:resistors:parallelR). From the colored bands, determine the resistances and set those same resistances and voltages in the PhET simulator.  Apply the input voltages as shown in [](#tab:resistors:singleR) and measure the currents at the locations indicated in [](#fig:resistors:parallelRImeas). These three currents should be different from one another. If you have any trouble, use the PhET simulation to help troubleshoot. Measure the voltage across each resistor (two voltage measurements).
```{figure} ../figures/ch2_resistors/parallelR.svg
:label: fig:resistors:parallelR
:width: 50%
:align: center
:alt: Circuit showing a two resistors in parallel connected to a battery or power source.
Circuit showing a two resistors in parallel connected to a battery or power source.
```
```{figure} ../figures/ch2_resistors/parallelR_Imeas.svg
:label: fig:resistors:parallelRImeas
:width: 50%
:align: center
:alt: Three locations identified for measuring current in the parallel circuit.
Three locations identified for measuring current in the parallel circuit.
```
```{exercise}
:label: exercise:resistor:parallelR
Using your results, show that $V=IR$ for each resistor within the uncertainty of the experiment.
```

(sec:resistors:vdivider)=
## Part 4 - Application: Voltage Divider to Measure Temperature

A voltage divider is a series resistor circuit. As you saw in [%s](#sec:resistors:part2), the voltage across resistors in series varies according to the values of resistance, i.e., a large resistor will have a proportionally larger voltage drop than a smaller resistor in a series connection. A voltage divider is shown in [](#fig:resistors:vdivider) and is the same circuit as [](#fig:resistors:seriesR).
### Voltage Divider Overview

A voltage divider has two essential parts: the circuit and the equation.

### The Circuit
A voltage divider is created by connecting two resistors in series across a voltage source. You might see this circuit drawn in slightly different ways, but the basic setup is always the same.
```{figure} ../figures/ch2_resistors/VDivider.svg
:label: fig:resistors:vdivider
:width: 50%
:align: center
:alt: A voltage divider circuit with an unknown resistor $R_T$.
A voltage divider circuit with an unknown resistor $R_T$.
```
We will label the resistor connected closest to the input voltage ($V_o$) as $R_T$, and the resistor connected closer to ground as $R_1$, where we know the input voltage and the resistance of $R_1$. $R_T$ is a variable resistance that changes with temperature. The voltage measured across $R_1$ is called $V_1$.

That's really all there is!
$V_1$ is the "divided" voltage — a specific fraction of the input voltage.

### The Equation
To use a voltage divider, you need to know three values. In this case, we know the input voltage ($V_o$), the resistor values $R_1$, and we measure the voltage across the known resistor $R_1$. With these, you can calculate the unknown resistance ($R_T$) using resistor circuit formulas.

Voltages sum:
```{math}
:label: eq:resistors:sumV
V_o = V_1 + V_T
```
Ohm's Law of equation {eq}`eq:resistors:ohms` for a series circuit is a constant current flowing through both resistors. We are free to substitute any $V$ with $IR$, where $I=V_o/R$ and $R=R_1+R_T$. Together, we can write
```{math}
:label: eq:resistors:vdivider
R_T = \left(\frac{V_o}{V_1}-1\right)R_1
```
The last equation in {eq}`eq:resistors:vdivider` shows that the unknown resistance can be calculated by measuring the voltage of the known resistor.

### The experiment

Measure the room temperature resistance of the thermal resistor with your multimeter. Choose a resistor for $R_1$ that is similar in resistance. Set up a voltage divider circuit with two resistors in series as shown in [](#fig:resistors:vdivider). Set $V_o=3 V$, and measure the voltage drop across $R_1$. Calculate the resistance of the thermal resistor $R_T$. Place the thermal resistor in three different environments, one hotter, one colder, and one equal to room temperature. Calculate the resistances of the thermal resistor. Repeat these measurements two more times.
```{exercise}
Describe the reproducibility of the thermal resistor to measure the same temperature.
```