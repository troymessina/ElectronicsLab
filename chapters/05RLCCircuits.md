---
title: Chapter 5 - Multistage RC and Single RLC Circuits
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:rlc)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments in with resistors, inductors, and  capacitors
* Students analyze data related to RC  and RLC circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

These experiments will continue using a FeelTech FY3200S signal generator and a Tektronix TBS 1072B-EDU digital oscilloscope to measure the waveforms connected to resistor, incductor, and capacitor circuits.

Part 1 of this lab is to measure and compare to a theoretical model the gain and phase of multistage RC circuits as shown in [](#fig:rlc:multirc). 
```{figure} ../figures/ch5_rlc/MultistageRC.svg
:label: fig:rlc:multirc
:width: 80%
:align: center
:alt: A multistage RC circuit.
A multistage RC circuit.
```

Part 2 of this lab is to measure and compare to a theoretical model the gain, phase, and resonance of RLC circuits like the one shown in [](#fig:rlc:rlc).

```{figure} ../figures/ch5_rlc/RLC.svg
:label: fig:rlc:rlc
:width: 40%
:align: center
:alt: A RLC oscillator circuit.
A RLC oscillator circuit.
```

# Procedure

## Part 1 - Theory of Multistage RC Circuits
We saw in the RC lab that the impedance of an RC circuit is
```{math}
Z &= X_R+X_C\\
Z &= R + \frac{1}{i\omega C}
```

In this lab we will use two different resistor/capacitor values for each stage, and we want the cross-over frequency ($f=1/RC$) to be the same for each stage to keep our analysis simple. We also want the first stage to define the current. To do this we choose $R_1\ll R_2$ or $R_2/R_1>10$. Since $1/R_1C_1 = 1/R_2C_2$, we will need to choose capacitors accordingly. More details are in the Measurements section.

In general, each loop’s current can be written
```{math}
I &= \frac{V}{Z}=V\left(\frac{1}{R+\frac{1}{i\omega C}}\right)\\
I &= \left(\frac{i\omega C}{1+i\omega RC}\right)V
```
For simplicity, let’s assume we can separate each stage for analysis. See [](#fig:rlc:sepmultirc). This shows that the voltage across $R_1$ is the input voltage to the second stage.
```{figure} ../figures/ch5_rlc/separatedmultistageRC.svg
:label: fig:rlc:sepmultirc
:width: 100%
:align: center
:alt: A separated multistage RC circuit.
A separated multistage RC circuit.
```

According to Ohm’s Law, the voltage across the resistor is
```{math}
V_{R_1}=I_1R_1=\frac{i\omega C_1}{1+iR_1C_1}V_oR_1
```
Similarly, for R2
```{math}
V_{R_2}=I_2R_2=\frac{iC_2}{1+iR_2C_2}V_{R_1}R_2
```

We are interested in how the output relates to the input of the circuit. We can define a ratio of the output voltage to the input voltage.
```{math}
\frac{V_{R_2}}{V_o} &= \frac{V_{R_2}}{V_{R_1}}\cdot\frac{V_{R_1}}{V_o}\\
\frac{V_{R_2}}{V_o} &= \frac{i\omega R_2C_2}{1+i\omega R_2C_2}\cdot\frac{i\omega R_1C_1}{1+i\omega R_1C_1}
```
This is a complex function, and in the real world we can only measure real values. Therefore, we need to calculate the gain of the circuit by calculating the magnitude of this complex function.
```{math}
{\rm Gain} = \left|\frac{V_{R_2}}{V_o}\right|
```
When calculating the magnitude of a complex function, we complex square it and take the square root. First, the two terms need to be written in the form
```{math}
z = a\pm ib
```
Then, the magnitude is
```{math}
\left| z\right| = \sqrt{\left(a+ib\right)\left(a-ib\right)}
```
After some algebra, you should find
```{math}
{\rm Gain} = \left|\frac{V_{R_2}}{V_o}\right| = \frac{\omega R_2C_2}{\sqrt{1+\omega^2R_2^2C_2^2}}\cdot\frac{\omega R_1C_1}{\sqrt{1+\omega^2R_1^2C_1^2}}
```
```{exercise}
* Work out the mathematics starting from the voltage across each resistor to show this is the gain of the circuit.
* Work out the mathematics to show this is the phase of the circuit.
```

The phase for this circuit can be expressed as
```{math}
\phi = \tan^-1\left(\frac{1}{\omega R_1C_1}\right)+\tan^-1\left(\frac{1}{\omega R_2C_2}\right)
```

(sec:rlc:part1meas)=
## Part 1 - Measurements
As observed in [](#sec:oscopes:sigintegrity), the function generators work well from 1 Hz to 10 MHz. Choose the cross-over frequency such that it will be in the middle of this range on a log-scale. That is, choose components such that 
```{math}
\omega = \frac{1}{R_1C_1}=\frac{1}{R_2C_2} \approx 10 {~\rm krad/s}
```
and
```{math}
50\Omega\ll R_1 \ll R_2 \ll 1 M\Omega
``` 
```{exercise}
Show calculations of expected resistor and capacitor cross-over frequencies based on your choices. Write down actual values for each component as measured by a digital multimeter.
```
Set up your circuit and measure the gain and phase as a function of frequency
```{exercise}
* Plot the gain and phase as functions of log($\omega$) using the resistor and capacitor values you choose in [](#sec:rlc:part1meas). Code to assist you is shown below.
* Comment on the accuracy of the theoretical models.
```

```{code-cell} Python
import matplotlib.pyplot as plt
import numpy as np

# theoretical data
omega = np.linspace(0,100000, 100001)
R1 = 1000
R2 = 10000
C1 = 1e-7 #100 nF
C2 = 1e-8 #1nF
print(1/R1/C1, 1/R2/C2)
gain_theory = omega*R1*C1/np.sqrt(1+(omega*R1*C1)**2) * omega*R2*C2/np.sqrt(1+(omega*R2*C2)**2)
phase_theory = np.atan(1/(omega*R1*C1)) + np.atan(1/(omega*R2*C2))

# experimental data
omega_exp = np.array([])
gain_exp = np.array([])
phase_exp = np.array([])

fig, (ax1, ax2) = plt.subplots(2, 1, sharex=True)

ax1.semilogx(omega, gain_theory, '-k', label='Theoretical Gain')
ax1.semilogx(omega_exp, gain_exp, 'ob', label='Experimental Gain')
ax1.set_ylabel('Theoretical Gain')
ax1.legend()
ax2.semilogx(omega, phase_theory, '-k', label='Theoretical Phase')
ax2.semilogx(omega_exp, phase_exp, 'ob', label='Experimental Phase')
ax2.set_ylabel(r'Phase, $\phi$ (rad)')
ax2.legend()
plt.xlabel(r'log($\omega$)')
plt.show()
```

## Part 2 - Theory of RLC Circuits

Inductors are a  circuit component you likely have not encountered. It is essentially a coil of wire with a  magnetic core to enhance its strength. See [](#fig:rlc:inductor.svg).

```{figure} ../figures/ch5_rlc/inductors.svg
:label: fig:rlc:inductor
:width: 80%
:align: center
:alt: The makeup of an inductor includes a wire coil wrapped around a core material. (a) A solenoidal type inductor. (b) A toroidal type inductor.
The makeup of an inductor includes a wire coil wrapped around a core material. (a) A solenoidal type inductor. (b) A toroidal type inductor. 
```

A voltage applied across an inductor creates a magnetic field along the inductor. The strength of the field or magnetic flux is related to the voltage, cross-sectional area, length, and number of turns.

We define inductance, $L$, as
```{math}
L=\frac{\Phi}{I} = \frac{\mu N^2 \pi R^2}{\ell}
```
Where $\Phi$ is the magnetic flux and $I$ is the current through the coil. The relationship for an inductor that is similar to Ohm’s Law comes from Faraday’s Law of Induction
```{math}
V &= -\frac{d\Phi}{dt}\\
V &= -L\frac{dI}{dt}
```
This equation says that changes in current through an inductor cause a counter emf ($V$). It should be immediately obvious that the voltage and current will be phase-shifted for an AC signal in an inductor circuit. The impedance of an inductor can be found similarly to what we did with capacitors. Assume we have a sinusoidal current.
```{math}
V(t) = -L\frac{d}{dt} I_o\sin\left(\omega t\right) = -\omega L I_o \cos\left(\omega t\right)
```
Thus, the inductor equivalent of Ohm’s Law gives a maximum  impedance of
```{math}
Z_L= -\omega L
```

In this lab, we will look at an RLC circuit that acts like an electronic damped oscillator. To analyze this circuit [](#fig:rlc:rlc), we consider Kirchoff’s voltage law
```{math}
V_o &= V_R + V_L + V_C\\
V_o\cos\left(\omega t\right) &= IR + L\frac{dI}{dt} + QC
```
To put this in terms of a common variable ($I$) we differentiate with respect to time to obtain
```{math}
-\omega V_o \sin\left(\omega t\right) = R\frac{dI}{dt} + L\frac{d^2I}{dt^2} + IC
```

This is a second order differential equation that applies to any driven harmonic oscillator, where the left hand side is the driving “force” and the right hand side is the dissipative ($R$), accelerative ($L$), and restoring ($C$) “force” terms. I use quotes because this is not a force equation, but there is an analogous force equation for a spring mass system. We can guess a solution of the form
```{math}
I(t) =I_o\cos\left(\omega t- \phi\right)
```
where $\phi$ is a phase that may be caused by differences in voltage and current like we saw with capacitors. Plugging this solution into the differential equation and doing some algebra, we obtain
```{math}
\begin{align}
& I_o\left[\left(\omega L - \frac{1}{\omega C}\right)\cos\left(\phi\right)-R\sin\left(\phi\right)\right]\cos\left(\omega t\right) + \cdots\\\\ & I_o\left[\left(\omega L - \frac{1}{\omega C}\right)\sin\left(\phi\right) + I_oR\cos\left(\phi\right)-V_o\right] \sin\left(\omega t\right) = 0
\end{align}
```
The time dependent functions are orthogonal to one another, i.e., the integral of their product over all space is zero. This means the only way for the above equation to be true is if the coefficients are equal to zero. We will assume $I_o\neq 0$.
```{math}
\left(\omega L - \frac{1}{\omega C}\right)\cos\left(\phi\right)-R\sin\left(\phi\right) &= 0\\
\left(\omega L - \frac{1}{\omega C}\right)\sin\left(\phi\right) + I_oR\cos\left(\phi\right)-V_o &= 0
```
From the first equation, we obtain the phase
```{math}
\boxed{\tan\left(\phi\right) = \frac{\omega L-\frac{1}{\omega C}}{R}}
``` 
$L$, $R$, and $C$ are fixed from the components used. The frequency will always be greater than 1. As $\omega$ increases, the dominant term changes as shown in [](#fig:rlc:rlctwoterms). This cross-over point changes the phase from negative to positive, i.e., a lead to a lag in the current.
```{figure} ../figures/ch5_rlc/phaseterms.svg
:label: fig:rlc:rlctwoterms
:width: 80%
:align: center
:alt: A log-plot of the two terms on the right hand side of the RLC phase equation with $L=100~\mu{\rm H}, C=1 \mu{\rm F}, R=1000 \Omega$.
A log-plot of the two terms on the right hand side of the RLC phase equation with $L=100~\mu{\rm H}, C=1 \mu{\rm F}, R=1000 \Omega$.
```

```{figure} ../figures/ch5_rlc/rlcphase.svg
:label: fig:rlc:rlcphase
:width: 80%
:align: center
:alt: A semilog plot of the phase vs. log(ω). The crossing point of the argument creates a plateau in the phase as the phase goes from current leading the input voltage to the current lagging the input voltage.
A semilog plot of the phase vs. log(ω). The crossing point of the argument creates a plateau in the phase as the phase goes from current leading the input voltage to the current lagging the input voltage.
```

From the second equation, we obtain the amplitude of the current.
```{math}
I_o=\frac{V_o}{\left(\omega L-\frac{1}{\omega C}\right)\sin\left(\phi\right) + R\cos\left(\phi\right)}
```
```{exercise}
Work out all of the above mathematics for phase and current filling in algebra steps.
```
Consider the impedance triangle shown in [](#fig:rlc:rlcphasetriangle).
```{figure} ../figures/ch5_rlc/rlcimpedancetriangle.svg
:label: fig:rlc:rlcphasetriangle
:width: 80%
:align: center
:alt: Impedance triangle for RLC circuit.
Impedance triangle for RLC circuit.
```
Based on the triangle we can rewrite the current using the magnitude of the impedance.
```{math}
I_o=\frac{V_o}{\sqrt{R^2+\left(\omega L-\frac{1}{\omega C}\right)^2}}
```
The denominator happens to be the magnitude of the complex impedance
```{math}
Z = R + i\omega L + \frac{1}{i\omega C}
```
and therefore, the current is simply voltage divided by impedance, very similar to Ohm’s Law for a series circuit. A graph of the current vs. log() is shown in [](#fig:rlc:rlccurrent).
```{figure} ../figures/ch5_rlc/rlccurrent.svg
:label: fig:rlc:rlccurrent
:width: 80%
:align: center
:alt: Plot of the current flowing through the RLC circuit as a function of input frequency. Parameters are defined in [](#fig:rlc:phaseterms) and $V_o = 10$ V. A broad resonance is observed from about $10^4-10^6$ rad/s.
Plot of the current flowing through the RLC circuit as a function of input frequency. Parameters are defined in [](#fig:rlc:phaseterms) and $V_o = 10$ V. A broad resonance is observed from about $10^4-10^6$ rad/s.
```
All driven oscillators will display resonance when driven at the resonant frequency. The resonant frequency for an RLC circuit is 
```{math}
\omega_o=\frac{1}{\sqrt{LC}}
```
The resistor dissipates energy in the circuit making the circuit a damped oscillator. The damping coefficient is
```{math}
\alpha =\frac{R}{2L}
```
A final parameter describing an oscillator is its quality factor. The quality factor is ratio of energy stored to energy dissipated over one cycle of the AC input. The higher the quality factor the sharper the resonance. For an RLC series circuit, the quality factor is described as
```{math}
\boxed{Q=\frac{\omega_o L}{R}}
```
As an example, the quality factor for [](#fig:rlc:rlccurrent) is
```{math}
Q=\frac{\omega_o L}{R}=\frac{\sqrt{L}}{R\sqrt{C}}=\frac{\sqrt{0.0001}}{1000\sqrt{0.000001}}=0.01
```
[](#fig:rlc:rlccurrentcompare) shows how changing the resistor by a factor of 100 affects the quality factor. 
```{figure} ../figures/ch5_rlc/currentcompare.svg
:label: fig:rlc:rlccurrentcompare
:width: 80%
:align: center
:alt: Plot of the current flowing through the RLC circuit as a function of input frequency Parameters are defined in [](#fig:rlc:phaseterms) and $V_o= 10$ V. The resistance is changed for comparison of quality factor from 1000 Ω to 10 Ω.
Plot of the current flowing through the RLC circuit as a function of input frequency Parameters are defined in [](#fig:rlc:phaseterms) and $V_o= 10$ V. The resistance is changed for comparison of quality factor from 1000 Ω to 10 Ω.
```

A graphical way to think about the quality factor is the frequency of the resonance divided by the width of the resonance.
```{math}
\boxed{Q=\frac{\omega_o}{\Delta\omega}}
```
An example of estimating this from a graph would be to observe that the center resonance of the $R=1000~\Omega$ circuit is at $\omega_o=10^5~{\rm rad/s}$. The width of the resonance, which is calculated at $I_{max}/2=0.707\times 10^{-5}~{\rm A}$. Therefore, $\Delta\omega=0.65\times 10^7-1.5\times 10^5 = 6.35\times 10^6~{\rm rad/s}$. See [](#fig:rlc:reswidth) where the width $\Delta\omega$ is shown by a horizontal arrow at the appropriate height on the graph.
```{math}
Q=\frac{\omega_o}{\Delta\omega}=\frac{10^5}{6.35\times 10^6}=0.016
```
```{figure} ../figures/ch5_rlc/rlcresonancewidth.svg
:label: fig:rlc:reswidth
:width: 80%
:align: center
:alt: Plot of the current flowing through the RLC circuit as a function of input frequency Parameters are defined in Figure 5 and Vo= 10 V. The width of the resonance is shown as a horizontal black line.
```
## Part 2 - Measurements

Set up the circuit shown in [](#fig:rlc:rlc). Use values of $R$, $L$, and $C$ such that the resonant frequency is $10 < f < 100~{\rm  kHz}$. You will be using a 230 μH inductor because that’s what we have. Using a signal generator with a 10 Volt peak-to-peak sine wave and oscilloscope measure the phase and current as a function of frequency. You will need to split the input signal so that you can connect a BNC to BNC for phase measurements. Note: You will measure current on the oscilloscope as $I = V_R/R$.
```{exercise}
* Make graphs like those in Figs. 6 and 8. Be sure to create a theoretical function to graph over your data.
* Calculate theoretical values for ωo,α, and Q. Compare ωo and Q to what you would get from graphical analysis.
```
Put a smaller resistor of approximately 10 Ω. Change the input to a square wave and see if you can find the damped oscillations on the oscilloscope. It is interesting that a square wave which is a +/- DC signal would create a sinusoidal response. That is the resonant oscillator in action. Damped oscillations look like the signal in Figure 11.



Figure 11. A plot of the damped oscillating output signal.
Deliverable 7: Show the instructor your damped oscillations on the oscilloscope.
Challenge #1
The RLC circuit is sometimes called a “notch filter” because it only allows a specific frequency range to transmit with efficiency. Create a circuit that would transmit a frequency of 10 kHz with the highest Q you can achieve.
