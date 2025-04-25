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

All of the experiments will have a virtual component to accompany the work on the lab bench. The virtual experiments are done using the PhET simulator below. Click on the "Lab" tab. 

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
Explain how an increase in the current (number of charges flowing per second, not the speed of the charges) is a response to increasing voltage described by conservation of energy.
```

## Circuit Loop Rules
The word circuit comes from the idea that electronics make loops. A circuit or electronic loop must conserve energy. This leads to two circuit rules.
1.	The sum of voltages around a loop are zero, e.g., energy in from a battery equals energy out dissipated by a resistor.
2.	The current through a circuit or electronic loop is constant.
In [](#fig:resistors:singleR), on the left is a circuit shown as we might see in the lab with a battery and a resistor. On the right is the equivalent circuit diagram. We assume wires are ideal, with zero resistance.
```{figure} ../figures/ch2_resistors/singleR.png
:label: fig:resistors:singleR
:width: 80%
:align: center
:alt: Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
```

```{exercise}
* In your lab notebook, make a note of what battery and resistor circuit diagrams look like. 
* Which side of the battery is +, and which side is -? 
* How is this polarity indicated in the circuit diagram on the right?
```

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
* Calculate the resistance of the resistor shown in [](#fig:resistors:exampleBands) with green, blue, orange, and gold bands.
* Suppose this resistor is connected to a 3 Volt battery like the image of a circuit above. Using Ohm's Law in equation {eq}`eq:resistors:ohms`, what current will flow through the circuit?
```

# Experiment
## Part 1 – Single Resistor

Set up the circuit shown above with a single resistor in the simulator and on the lab bench. From the colored bands, determine the resistance and set the same resistance in the simulator. On the lab bench, you will use a power supply instead of a battery so that you can adjust the voltage. Apply the voltages as shown in the table below and measure the current flows for each applied voltage.
| Voltage (V) | Current (A) |
|:-----------:|:-----------:|
|      0.5    |             |
|      1.0    |             |
|      1.5    |             |
|      2.0    |             |
|      2.5    |             |
|      3.0    |             |
```{exercise}
:label: exercise:resistor:singleR
* Plot V vs I. What is the slope of your graph including uncertainty (We will go over graphing and fitting in Python.)? 
* How does your slope compare to the theoretical value of the resistor from its bands including uncertainty? Does the simulation give the same results as your experiment? Explain.
```

## Part 2 – Series Resistor
Set up a "series" circuit with two resistors in series as shown below. From the colored bands, determine the resistances and set those same resistances and voltages in the simulator.  Apply the voltages as shown in the table and measure the currents at the locations indicated (1-4) in the simulation. Measure the current anywhere on the real circuit. Measure the voltage across each resistor (two voltage measurements).

