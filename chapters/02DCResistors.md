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
#Background
Ohm’s Law says $V = IR$, or voltage equals the current times the resistance. $V$ is in Volts (Volts are Joules/Coulomb). $I$ is in amperes (or Coulomb per second), and $R$ is in Ohms (units you could work out from the others). These are SI units. Voltage, also called electric potential, is the source of energy pushing electrons through a typical circuit. Flowing charges, or current, is a result of the voltage pushing charges against electrical resistance. As voltage increases, the current should increase linearly for a particular resistance.
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
:width: 60%
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
:width: 60%
:align: center
:alt: Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
Circuit showing a single resistor connected to a battery or power source. On the right is the PhET cartoon with a battery and 10 Ohm resistor. On the left is the circuit diagram.
```
