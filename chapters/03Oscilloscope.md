---
title: Chapter 3 - Oscilloscopes and Signal Generators
numbering:
  headings:
  heading_1:
    start: 4
---
(chap:oscopes)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students understand the use of signal generators and oscilloscopes to set up experiments in signal analysis.
* Students understand data analysis related to Ohm’s Law and signal integrity.
* Students articulate results of AC experiments including experimental uncertainty.
:::

# Introduction
Producing electronic signals for circuits and measuring input and output signals of electronics circuits is important for a wide variety of applications. Everything from power lines to cell phones to Fitbits use electronic signals and circuits. This lab will explore signals and their measurement. We will use a FeelTech FY3200S [](#fig:oscopes:signalgen) signal generator capable of producing alternating signals in sine, square, triangle, and arbitrary formats. We will use a Tektronix TBS 1072B-EDU [](#fig:oscopes:oscope) digital oscilloscope to measure the waveforms from the signal generator (input) and from simple circuits (output).
```{figure} ../figures/ch3_oscopes/FeelTech.jpg
:label: fig:oscopes:signalgen
:width: 60%
:align: center
:alt: The FeelTech FS3200 signal generator.
The FeelTech FS3200 signal generator.
```
```{figure} ../figures/ch3_oscopes/Tektronix.jpg
:label: fig:oscopes:oscope
:width: 60%
:align: center
:alt: The Tektronix 1102BEDU oscilloscope.
The Tektronix 1102BEDU oscilloscope.
```
Part 1 of this lab is to measure the output impedance of the FeelTech signal generator. The output impedance is a measure of the source's propensity to drop in voltage when the load draws current, the source being the portion of the circuit that transmits and the load being the portion of the circuit that consumes. Because of this the output impedance is sometimes referred to as the source impedance or internal impedance.

Part 2 of this lab is to measure the integrity of the signal generator. We will do this by looking at the accuracy of the frequency and the rise time of a square wave.


Procedure
