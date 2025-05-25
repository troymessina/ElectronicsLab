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
* Students analyze data related to op amp circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

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
