---
title: Chapter 8 - Operational Amplifiers
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:opamps)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments with operational amplifiers.
* Students analyze data related to op-amp circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

Operational amplifiers, or op-amps, are versatile analog circuit building blocks used in a wide variety of applications. They are essentially high-gain voltage amplifiers with differential inputs and a single-ended output.  The "operational" part of their name comes from their ability to perform various mathematical operations like amplification, addition, subtraction, integration, and differentiation when combined with external components.

**Key characteristics of an ideal op-amp include:**

-   **Infinite open-loop gain:** This allows for a large amplification of the difference between the two input voltages.
-   **Infinite input impedance:** No current flows into the inputs.
-   **Zero output impedance:** The op-amp can drive any load without voltage drop.
-   **Infinite bandwidth:**  The op-amp can amplify signals of any frequency.

**In reality, op-amps deviate from these ideals:**

-   **Finite gain and bandwidth:**  Practical op-amps have a limited gain and bandwidth.
-   **Non-zero input and output impedance:**  Real op-amps have some input current and output impedance.
-   **Offset voltage:**  A small voltage difference may exist between the inputs even when the output is zero.
-   **Slew rate limitation:**  The output voltage cannot change instantaneously.

## Op-Amp Pinouts

A typical op-amp has the following pin configuration.
```{table} Numbering and function of pins on a DIP8 op-amp.
:label: table:opamps:pinout
:align: center
| Pin Number | Function |
|:---:|:---|
| 1 | Offset Null (Optional) |
| 2 | Inverting Input (-) |
| 3 | Non-inverting Input (+) |
| 4 | Negative Power Supply (V-) |
| 5 | Offset Null (Optional) |
| 6 | Output |
| 7 | Positive Power Supply (V+) |
| 8 | Not connected |
```

A diagram of an op-amp is shown in [](#fig:opamps:diagram). In [](#fig:opamps:diagram) (a), the DIP8 packaging is shown including the pin numbers of the visible pins. In [](#fig:opamps:diagram) (b) the circuit symbol of an op-amp is shown with the pin numbers identified. These three pins are the only pins relevant to the amplifier itself. The other pins are described in [](#sec:opamps:pinexplanation). In [](#fig:opamps:diagram) (c), the internal structure of the op-amp is shown with all of the pin numbers and functions labeled.
```{figure} ../figures/ch8_opamps/OpAmpDiagram.svg
:label: fig:opamps:diagram
:width: 75%
:align: center
:alt: Diagram of an operational amplifier. (a) The DIP8 packaging with some pin numbers identified. (b) The circuit symbol with pin numbers identified. (c) Schematic of the internal circuitry with pin numbers and functions identified.
Diagram of an operational amplifier. (a) The DIP8 packaging with some pin numbers identified. (b) The circuit symbol with pin numbers identified.[^1] (c) Schematic of the internal circuitry with pin numbers and functions identified.[^2]
```

(sec:opamps:pinexplanation)=
### Explanation of pins

-   **Inverting Input (-):** An input signal applied to this pin will be amplified and inverted at the output.
-   **Non-inverting Input (+):specifies:** An input signal applied to this pin will be amplified without inversion at the output.
-   **Output:**  The amplified signal is available at this pin.
-   **Positive and Negative Power Supply (V+ and V-):** These pins supply power to the op-amp.
-   **Offset Null (Optional):**  These pins can be used to adjust the output voltage to zero when no input signal is present, compensating for any inherent offset voltage.

**Note:** The pin configuration and numbering can vary slightly depending on the specific op-amp package (e.g., DIP, SOIC) and manufacturer. Always refer to the datasheet for the specific op-amp you are using.

# Theory

## Op Amp Current and Voltage Rules

Operational amplifiers (op-amps) are versatile analog circuit building blocks, and understanding their behavior requires adherence to fundamental current and voltage rules, particularly when configured with negative feedback.

### 1. The Golden Rules of Op-Amps:

These rules simplify the analysis of op-amp circuits with negative feedback:

*   **Rule 1 (Current Rule):** No current flows into either of the op-amp's input terminals (inverting and non-inverting). This stems from the ideal op-amp's infinite input impedance.

*   **Rule 2 (Voltage Rule):** The op-amp's output adjusts itself to ensure that the voltage difference between its two inputs is zero (V+ = V-). This is due to the op-amp's extremely high open-loop gain.

### 2. The Concept of Virtual Short (or Virtual Ground):

*   When negative feedback is applied, and the non-inverting input is connected to a fixed voltage (like ground), the inverting input is forced to be at the same potential as the non-inverting input.
*   This condition is termed a "virtual short" because the inputs are not physically connected, yet their voltages are effectively equal. If the non-inverting input is grounded, the inverting input is said to be at "virtual ground".

### 3. Consequences of the Golden Rules:

*   **Current Flow:** The current in an op-amp circuit with negative feedback is determined by the external components (resistors, capacitors, etc.) connected in the feedback network, not by the op-amp itself.
*   **Gain and Feedback:** The gain of the op-amp circuit is primarily determined by the feedback network. Negative feedback stabilizes the gain and makes it less dependent on the op-amp's open-loop gain.
*   **Input and Output Impedance:** Negative feedback also influences the circuit's input and output impedance. For instance, in a non-inverting amplifier, negative feedback increases the input impedance and decreases the output impedance.

## Summary

*   Op-amp circuits with negative feedback are analyzed using the "golden rules" that simplify calculations and predictions of circuit behavior.
*   The virtual short concept is a powerful tool for analyzing circuits, enabling engineers to treat the input terminals as having the same voltage even though they are not physically connected.
*   Negative feedback is crucial for controlling gain, improving stability, and achieving desired impedance characteristics in op-amp circuits.

In this experiment, we will be building different circuits that will demonstrate the
usefulness and simplicity of using operational amplifiers.

# Experiment

## Inverting Amplifier

The circuit shown in [](#fig:opamps:invertingamp) is an inverting amplifier. The resistor $R_F$ provides negative feedback, which is the process of “feeding back” a fraction of the output signal back to the input. The feedback is negative because we must feed it back to the “inverting input” terminal of the op-amp. This feedback connection between the output and the inverting input terminal forces the differential input voltage towards zero due to the voltage rule of op-amps.
```{figure} ../figures/ch8_opamps/invertingamplifier.svg
:label: fig:opamps:invertingamp
:width: 75%
:align: center
:alt: An inverting amplifier op-amp circuit.
An inverting amplifier op-amp circuit.
```

This is a closed loop amplifier circuit that produces gain referred to as closed-loop gain. A closed-loop inverting amplifier uses negative feedback to accurately control the overall gain of the amplifier, but at a cost in the reduction of the amplifiers gain.

This negative feedback results in the inverting input terminal having a different signal on it than the actual input voltage as it will be the sum of the input voltage plus the negative feedback voltage giving it the label or term of a Summing Point. We must therefore separate the real input signal from the inverting input by using an input resistor, $R_{in}$.

The positive, non-inverting input is connected to a common ground or zero voltage. The effect of this closed loop feedback circuit results in the voltage at the inverting input being equal to that at the non-inverting input producing a virtual ground summing point because it will be at the same potential as the grounded non-inverting input. The op-amp becomes a “differential amplifier”.

Because of the op-amp rules, we can use an equivalent circuit shown in [](#fig:opamps:invertingampequiv) to analyze the expected measurements.
```{figure} ../figures/ch8_opamps/invertingamplifierequiv.svg
:label: fig:opamps:invertingampequiv
:width: 75%
:align: center
:alt: An equivalent circuit diagram of the inverting amplifier.
An equivalent circuit diagram of the inverting amplifier.
```
The current through the resistors must be constant and therefore is
```{math}
:label: eq:opamps:invampcurr
I = \frac{V_{out}-V_{in}}{R_{in}+R_F}
```
We can also consider the current flowing through the individual resistors since we know $V_2=0$.
```{math}
I = \frac{V_2-V_{in}}{R_{in}}=\frac{V_{out}-V_2}{R_F}
```
Therefore,
```{math}
\frac{V_2-V_{in}}{R_{in}} &= \frac{V_{out}-V_2}{R_F}\\
\frac{-V_{in}}{R_{in}} &= \frac{V_{out}}{R_F}\\
\frac{V_{out}}{V_{in}} &= -\frac{R_F}{R_{in}}
 ```

Build the circuit in [](#fig:opamps:invertingamp) with resistors $R_{in}=1000~{\rm \Omega}$ and $R_F=1000~{\rm \Omega}$

### Application - Light Detection

## Non-inverting Amplifier



[^1]: By Inductiveload - Own work, Public Domain, https://commons.wikimedia.org/w/index.php?curid=8433629
[^2]: By Inductiveload - Self-made, Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=3439390