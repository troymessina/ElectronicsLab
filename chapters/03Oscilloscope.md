---
title: Chapter 3 - Oscilloscopes and Signal Generators
numbering:
  headings:
  heading_1:
    start: 3
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


# Procedure
Explore the signal generator.
:::{note} Deliverable 1
Explain the following.
* What does the PARM button do?
* What PARMs are available?
* How do you
	* Adjust the frequency?
	* Adjust the amplitude?
	* Change the waveform?
* If you adjust the frequency and push the blue knob, what happens?
* If you are adjusting any parameter and push the blue knob, what happens?
* What does the WAVE button do?
* How do you turn on/off CH1 and CH2?
* How do you select whether you are adjusting CH1 or CH2?
:::

## Part 1 - Signal Generator Output Impedance
Set up a signal generator and oscilloscope like the following diagram (Fig. 3). The output of the signal generator CH1 should be a 2 Volt peak-to-peak sine wave with a frequency of 1000 Hz.  Connect a BNC to alligator clip cable to CH1 on the signal generator. Connect a BNC to alligator clip to the oscilloscope channel 1 (yellow). Use the alligator clips to connect a 100Ω load resistor.
```{figure} 
:label: fig:oscopes:expsetup
:width: 100%
:align: center
:alt: The setup of the experiment. A signal generator connected to a load. The oscilloscope measures the voltage signal across the load. The load signal would be equal to the signal generator signal if there were no output impedance.
The setup of the experiment. A signal generator connected to a load. The oscilloscope measures the voltage signal across the load. The load signal would be equal to the signal generator signal if there were no output impedance.
```
```{figure} 
:label: fig:oscopes:expdiagram
:width: 60%
:align: center
:alt: Equivalent circuit showing a sine wave going through two resistors in series. The oscilloscope measures the voltage across the load, indicated by the circles.
Equivalent circuit showing a sine wave going through two resistors in series. The oscilloscope measures the voltage across the load, indicated by the circles.
```
Explore the oscilloscope
When you have your circuit connected, try to find the signal on the oscilloscope.
:::{note} Deliverable 2
Explain how to
* Select channel 1 (yellow).
* Move the signal left/right.
* Move the signal up/down.
* Zoom the signal in/out horizontally (time) and vertically (voltage).
* Measure the signal amplitude.
* Measure the signal frequency.
:::

### Measurements
Use at least 10 different load resistors between 10 and 100 000 Ω to measure $V_L$.

## Part 2 - Signal Integrity
Determine the accuracy of the frequency of the signal generator as a function of frequency. For a sine wave and a square wave of 2 Volts peak-to-peak, adjust the frequency using a log-scale, i.e., 10 Hz, 20 Hz, 50 Hz, 100 Hz, 200 Hz, 500 Hz, etc. up to 10 MHz. Record the signal generator frequency as your x-value and the oscilloscope value as your y-value. You will have two datasets, one for sine and one for square. Keep in mind you will need to adjust the horizontal scaling on the oscilloscope so that you can see at least one period of the wave. The oscilloscope will measure the frequency and period for you. However, you should include in your report how you can use the screen and scaling adjustments to get an accurate measurement manually.

When measuring the square wave, use the cursor capabilities on the oscilloscope to measure the time it takes the square wave to go from its highest to lowest point on the falling side of the square wave.

# Part 1 Theory
According to Ohm’s Law, we know

$$V=IR$$

We know from the equivalent circuit that the series resistance is

$$R=R_{out}+R_L$$

We also know for series resistors, the voltages sum to the input voltage

$$V=V_{out}+V_L$$

Finally, we know the current is the same throughout the circuit.
$$I=I_{out}=I_L$$

Deliverable 3: From these relationships show that

$$V_L=V\left(\frac{R_L}{R_{out}+R_L}\right)

:::{note} Deliverable 4
Explain why a plot of $1/V_L$ vs. $1/R_L$ is a good way to obtain $R_{out}$.
:::

# Results
Create a Colab (https://colab.research.google.com/)account with Google and copy this Jupyter notebook to your account. https://colab.research.google.com/drive/1vzdpEgh7kat6cTAndPkRkRC-yOkTxA2C?usp=sharing

```python
import numpy as np
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [1, 2, 3], 'go-', label='line 1', linewidth=2)
```

Enter your data into the arrays and make a graph for part 1 similar to what is shown below in Figure 5.
