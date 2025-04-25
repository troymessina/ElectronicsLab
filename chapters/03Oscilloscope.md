---
title: Chapter 3 - Oscilloscopes and Signal Generators
kernelspec:
  name: python3
  display_name: 'Python 3'
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
```{exercise}
:label: exercise:oscopes:deliverable1
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
```

## Part 1 - Signal Generator Output Impedance
Set up a signal generator and oscilloscope as shown in [](#fig:oscopes:expsetup). The equivalent circuit you are measuring is shown in [](#fig:ch3_oscopes/equivcircuit). The output of the signal generator CH1 should be a 2 Volt peak-to-peak sine wave with a frequency of 1000 Hz.  Connect a BNC to alligator clip cable to CH1 on the signal generator. Connect a BNC to alligator clip to the oscilloscope channel 1 (yellow). Use the alligator clips to connect a 100Ω load resistor.
```{figure} ../figures/ch3_oscopes/expsetup.jpg
:label: fig:oscopes:expsetup
:width: 100%
:align: center
:alt: The setup of the experiment. A signal generator connected to a load. The oscilloscope measures the voltage signal across the load. The load signal would be equal to the signal generator signal if there were no output impedance.
The setup of the experiment. A signal generator connected to a load. The oscilloscope measures the voltage signal across the load. The load signal would be equal to the signal generator signal if there were no output impedance.
```
```{figure} ../figures/ch3_oscopes/equivcircuit.jpg
:label: fig:oscopes:equivcircuit
:width: 60%
:align: center
:alt: Equivalent circuit showing a sine wave going through two resistors in series. The oscilloscope measures the voltage across the load, indicated by the circles.
Equivalent circuit showing a sine wave going through two resistors in series. The oscilloscope measures the voltage across the load, indicated by the circles.
```
### Explore the oscilloscope
When you have your circuit connected, try to find the signal on the oscilloscope.
```{exercise}
:label: exercise:oscopes:deliverable2
Explain how to
* Select channel 1 (yellow).
* Move the signal left/right.
* Move the signal up/down.
* Zoom the signal in/out horizontally (time) and vertically (voltage).
* Measure the signal amplitude.
* Measure the signal frequency.
```

### Measurements
Use at least 10 different load resistors between 10 and 100 000 Ω to measure $V_L$.

## Part 2 - Signal Integrity
Determine the accuracy of the frequency of the signal generator as a function of frequency. For a sine wave and a square wave of 2 Volts peak-to-peak, adjust the frequency using a log-scale, i.e., 10 Hz, 20 Hz, 50 Hz, 100 Hz, 200 Hz, 500 Hz, etc. up to 10 MHz. Record the signal generator frequency as your x-value and the oscilloscope value as your y-value. You will have two datasets, one for sine and one for square. Keep in mind you will need to adjust the horizontal scaling on the oscilloscope so that you can see at least one period of the wave. The oscilloscope will measure the frequency and period for you. However, you should include in your report how you can use the screen and scaling adjustments to get an accurate measurement manually.

When measuring the square wave, use the cursor capabilities on the oscilloscope to measure the time it takes the square wave to go from its highest to lowest point on the falling side of the square wave.

# Part 1 Theory
According to Ohm’s Law, we know

```{math}
:label: eq:oscopes:ohms
V=IR
```

We know from the equivalent circuit that the series resistance is

```{math}
:label: eq:ocsopes:seriesR
R=R_{out}+R_L
```

We also know for series resistors, the voltages sum to the input voltage

```{math}
:label: eq:oscopes:seriesV
V=V_{out}+V_L
```

Finally, we know the current is the same throughout the circuit.
```{math}
:label: eq:oscopes:constcurr
I=I_{out}=I_L
```

```{exercise}
:label: exercise:oscopes:deliverable3
From equations {eq}`eq:oscopes:ohms` through {eq}`eq:oscopes:constcurr`, show that

$$V_L=V\left(\frac{R_L}{R_{out}+R_L}\right)$$
```
```{exercise}
:label: exercise:oscopes:deliverable4
Explain why a plot of $1/V_L$ vs. $1/R_L$ is a good way to obtain $R_{out}$.
```

# Results

## Part 1
Enter your data into the arrays and make a graph for part 1 using the Python code shown below.
```{code-cell} python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

#define a linear function
def line_fit (x, m, b):
	return m*x + b

#Define your data
Rload = np.array([10., 15., 27., 33., 47., 68., 100., 150., 330., 470., 680., 1000., 10000., 22000.])
Rload_unc = 0.05*Rload #gold band resistors
Vload=np.array([0.38, 0.52, 0.74, 1.08, 1.02, 1.20, 1.40, 1.56, 1.84, 1.88, 1.94, 1.98, 2.06, 2.08])
Vload_unc = np.array([0.1,0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1])

#Do the linear fit
parms, cov = curve_fit(line_fit, Rload, Vload,sigma=Vload_unc, absolute_sigma=True)
print(parms, np.sqrt(cov))

plt.errobar(1/Rload, Vload, yerr=Vload_unc/Vload**2) #plot the data
plt.plot(1/Rload, parms[0]*1/Rload+parms[1])
plt.xlabel(r'$1/R_{load}$')
plt.ylabel(r'$1/V_{load}$')
plt.show()
```


