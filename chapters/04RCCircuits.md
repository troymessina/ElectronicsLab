---
title: Chapter 4 - RC Circuits
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:rc)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments in with resistors and capacitors
* Students analyze data related to RC circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

We will continue using a FeelTech FY3200S signal generator and a Tektronix TBS 1072B-EDU digital oscilloscope to measure the waveforms connected to series resistor and capacitor circuits.

Part 1 of this lab is to measure and compare peak-to-peak and rms voltages. The peak-to-peak voltage is the actual amplitude of an alternating signal between the highest peak to the lowest peak. Diagrams of three waveforms (sine, square, and triangle) are shown in [](#fig:rc:waves). The period and peak-to-peak voltage are labeled.
```{figure} ../figures/ch4_rc/waves.svg
:label: fig:rc:waves
:width: 100%
:align: center
:alt:A (a) sine wave, (b) square wave, and (c) triangle wave form. The rms voltages are $V_{rms}=V/\sqrt{2}=V_{pp}/2\sqrt{2}$ for the sine waveform, $V_{rms}=V=V_{pp}/2$ for the square waveform, and $V_{rms}=V/\sqrt{3}=V_{pp}/2\sqrt{3}$ for the triangle waveform.
A (a) sine wave, (b) square wave, and (c) triangle wave form. The rms voltages are $V_{rms}=V/\sqrt{2}=V_{pp}/2\sqrt{2}$ for the sine waveform, $V_{rms}=V=V_{pp}/2$ for the square waveform, and $V_{rms}=V/\sqrt{3}=V_{pp}/2\sqrt{3}$ for the triangle waveform.
```

Part 2 of this lab is to measure the response or output of series resistor and capacitor (RC) circuits when given DC or AC input.

# Procedure
## Part 1 Theory of RMS Voltage
Periodic voltages without DC voltage contribution such as sine-, square- or triangular- wave voltages, see Fig. 2, are characterized by the period T, frequency f = 1/T, amplitude V, peak-to-peak value Vpp = 2V, and rms value Vrms. The rms value corresponds to the value of a DC voltage which – at a given electrical resistance – leads to the same dissipated power as the AC voltage. The rms voltage can be calculated by averaging the square of the AC voltage, V(t):
```{math}
:label: eq:rc:rms
V_{rms} = \sqrt{\langle V^2\rangle}=\sqrt{\frac{1}{T}\int_0^T \left(V(t)\right)^2 dt}
```
where $\langle V^2\rangle$ is the average of the voltage squared. Evaluation of this integral leads to different effective values for the voltage-time characteristics as shown in [](#fig:rc:waves).

## Part 1 Measurements
Create each of these signals as with the signal generator such that they are $V_{pp}=5$ Volts for a frequency of $f=1000$ Hz. Connect a BNC to alligator clips cable to the signal generator. Measure the rms voltage using a multimeter set to AC Volts. Connect a BNC to BNC cable so that you can measure the signal on the oscilloscope. Adjust your oscilloscope such that you see approximately 2 periods of the wave. Repeat these activities for 100 Hz. You should include estimated uncertainties.
```{exercise}
Create a table like [](#tab:rc:rmsV) and comment on any apparent discrepancies or frequency dependence.
```
```{table} Comparison of peak-to-peak and rms voltages at 1 kHz and 100 Hz.
:label: tab:rc:rmsV
:align: center
| Signal Wave | RMS Voltage | Peak-to-peak Voltage |
|:------------|:------------|:---------------------|
|     Sine    |             |                      |
|    Square   |             |                      |
|   Triangle  |             |                      |
```

## Part 2a Theory of RC Circuits
A series circuit consists of a resistance, $R$, and a capacitor, $C$. Draw the circuit in your lab notebook including the AC input square wave. At $t = 0$ seconds a square voltage is applied to this circuit, such that a current $I(t)$ flows. This current charges the capacitor. The voltage across the capacitor $V_C(t)$ is measured over time and shows an increasing voltage with time from a value of zero approaching the applied voltage, $V_o$, of the square wave. According to Kirchhoff’s loop rules, the sum of the voltages across the capacitor and resistor must add to the applied voltage. The voltage on the capacitor has the form $V_C=Q/C$, and the resistor voltage is $V_R=IR$. Summing them gives
```{math}
:label: eq:rc:RCVsum
V_o=V_C+V_R=QC+IR
```
The current is the amount of charge flowing through the circuit per unit time, $I=dQ/dt$. Replace the current in the above equation to obtain a differential equation of $Q$. This leads to a linear, non-homogeneous differential equation of first order:
```{math}
:label: eq:rc:RCVsum2
V_o= QC +\left(\frac{dQ}{dt}\right)\cdot R
```
Solve this to obtain the time-dependent charging on the capacitor that can be converted to voltage on the capacitor
```{math}
:label: eq:rc:RCVcharge
\boxed{V_C(t)=V_o\left(1-e^{-t/RC}\right)}
```
Follow similar logic for discharging when the square wave goes to zero ($V_o = 0$) to obtain
```{math}
:label: eq:rc:RCVdicharge
\boxed{V_C(t)=V_o e^{-t/RC}=Voe^{-t/\tau}}
```
This result implies that there is a characteristic time for charging and discharging. This characteristic time is defined as the time when $t = \tau = 1/RC$. This simplifies the equation for capacitor voltage to
```{math}
:label: eq:rc:Vtau
V_C(\tau)=V_oe^{-1}=V_o e
```

In principle the capacitor needs infinitely long to charge or discharge, since the exponential function reaches zero only for infinitely long time spans. In the measurement, however, one obtains sufficiently good accuracy, when choosing the period of the square wave voltage such that it is large compared to the relaxation time, $\tau=RC$. If this condition is not fulfilled, the charging starts with a voltage $V_{min} > 0$ and reaches a voltage $V_{max} < V_o$ , i.e. the oscilloscope shows only a fraction of the charging and discharging of the capacitor's voltage-time curve.

## Part 2a - Measurements

Let’s set up the circuit and oscilloscope to observe this. You will need to add an offset such that the square wave has its minimum at zero. Once you have observed the effect, change the frequency of your input square wave so that the period is longer (~5-10 times) than the RC time constant. You can estimate this by calculating $\tau=RC$. The capacitor you have is $0.1 \mu F$. We will start with $R=10 k\Omega$. Then, adjust the frequency such that ($T = 1/f ~ 10RC$). What frequency is this? You should be able to adjust the oscilloscope to look like [](#fig:rc:rc). What X and Y settings are you using on your oscilloscope? Do these make sense? Explain.


```{figure} ../figures/ch4_rc/RC.svg
:label: fig:rc:rc
:width: 100%
:align: center
:alt: (a) A square wave input $V(t)$ (blue) and (b) output $V_C(t)$ (red) measured across a capacitor in an RC circuit.
(a) A square wave input $V(t)$ (blue) and (b) output $V_C(t)$ (red) measured across a capacitor in an RC circuit.
```
In order to get an accurate value of $\tau=RC$, we should zoom in on the charging and discharging as shown in [](#fig:rc:rczoom).
```{figure} ../figures/ch4_rc/RCzoom.svg
:label: fig:rc:rczoom
:width: 100%
:align: center
:alt: A close-up image of the charging and discharging capacitor circuit with a series resistor.
A close-up image of the charging and discharging capacitor circuit with a series resistor.
```

```{exercise}
* Explain your process for finding $\tau=RC$ and its uncertainty.
* What are your oscilloscope settings. Explain how your oscillosope settings make sense.
```
## Part 2b - Theory of AC Impedances
A single capacitor circuit with a sinusoidal input voltage will have a time-dependent voltage across the capacitor that is ideally
```{math}
V_C(t) =V_o \cos(t)
```
The current can be calculated by using the capacitor charge $Q =V/C$ and $I=dQ/dt$ to obtain
```{math}
I_C(t)=CV_o \sin(t)=CV_o \cos(t+\pi/2),
```
indicating a phase shift $\theta = \pi/2$ rad between the voltage and current on the capacitor. The maximum current is $I_{max}=\omega CV_o$, which comes from the amplitude of the derivative to find the time-dependent current. Similar to resistance in Ohm’s Law, there is a **capacitive reactance**, $X_C$, for the maximum current and voltage
```{math}
X_C=\frac{V_o}{I_{max}}=\frac{1}{\omega C}
```

Capacitive reactance is a resistance to voltage changes rather than resistance to current changes as observed in a resistor. Because it is a type of resistance, it can be added to resistor resistance as a **total impedance**, $Z$, of an RC circuit. The equation above is only a relationship for the maximum values of voltage and current due to the phase difference between the time-dependent values. Using the idea that the two impedance values are 90$^$\circ}$ out of phase means they can be treated like orthogonal vectors (phasors) - see [](#fig:rc:phasor). We can compute the total impedance using something analogous to the Pythagorean Theorem.

```{figure} ../figures/ch4_rc/ImpedancePhase.svg
:label: fig:rc:phasor
:width: 100%
:align: center
:alt: A diagram of impedance phasors.
A diagram of impedance phasors.
```

The voltage is a sum of the voltages on the resistor and capacitor (circuit loop rule 1). In a simple resistor circuit the voltage and current would follow one another as $V_o \cos(t)$. As noted above the voltage and current for a capacitor are 90$^$\circ}$ out of phase. 


Where the imaginary $i$ indicates an independent vector (phasor) direction that is due to the frequency dependence of the capacitor impedance. For a series circuit, we can describe the total impedance by
```{math}
Z^2_{total}= X^2_R + X^2_C
```

The magnitude of each impedance determines the phase angle between input voltage and the voltage across the resistor in the circuit. The current in the circuit can be measured by the voltage drop in the resistor because there is no phase added by the resistor. Using [](#fig:rc:phasor) one can find a relationship between the impedances


From this, we can define a crossover frequency when ω = 1/RC, θ = 45o. This is where the resistor voltage equals the capacitor voltage (see Fig. 6). The phase will be between 0 and 90o depending on ω, R, and C, and you will see something like Fig. 5 on your oscilloscope.
```{figure} ../figures/ch4_rc/RCPhaseShift.svg
:label: fig:rc:phaseshift
:width: 80%
:aligh: center
:alt: A plot showing the phase shift in a series RC circuit. The phase shift is  $\Delta t$.
A plot showing the phase shift in a series RC circuit. The phase shift is  $\Delta t$.
```

We can make substitutions to derive the maximum current in the circuit

and the maximum voltage on the resistor

and capacitor


Part 2b - Measurements
Use the oscilloscope to verify these relationships by setting Vo=5 V and measuring VR and VC at 100 Hz and 500 Hz using C = 0.1 μF and R = 10 kᘯ. Draw waveforms in your lab notebook. Next, use your oscilloscope to measure VR and VC as a function of ω. Plot on the same graph VR vs. ω and VC  vs. ω. They should look like the graph below. Plot the functions above on top of your data and comment on the accuracy of the theoretical model.




Figure 6. The voltages across a resistor (blue) and capacitor (orange) in a series circuit as a function of input sinusoidal frequency, ω.

Because the resistor voltage increases with frequency, it can be used as a high-pass filter, passing only voltages of high frequency. Contrary to the resistor, the capacitor passes only low frequency voltages. It can therefore be used as a low-pass filter.

Deliverable 4: Show the mathematical work to obtain the resistor and capacitor voltage equations above.
Deliverable 5: Make the measurements to make a graph like Figure 6. Use Colab and qexpy to produce all graphs in this lab.
Challenge #1
Create a circuit that might turn on a lamp to mimic the sunrise. It should slowly charge a capacitor over approximately 30 minutes. Explain how you designed, built, and tested this circuit.
Challenge #2
Create a circuit that could be used for tone adjustment on a guitar. Using variable resistors and regular capacitors, make a high pass and a low pass filter for a single AC input.

