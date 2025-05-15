---
title: Chapter 6 - Diodes
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:diodes)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments in with resistors, diodes, and photovoltaic cells.
* Students analyze data related to diode circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

We will switch to DC measurements for most of this lab. Toward the end, we will see how to automate our DC measurements using a function generator and oscilloscope. However, we will use a Data Acquisition (DAQ) system and LabVIEW software to do these measurements.

Part 1 of this lab is to measure and compare different types of diodes using a DC power supply and a digital multimeter. Diodes behave differently when forward biased or reversed biased. We will use a voltage divider circuit as shown in [](#fig:diodes:diodeVdivider).

```{figure} ../figures/ch6_diodes/diodeVdivider.svg
:label: fig:diodes:diodeVdivider
:width: 50%
:align: center
:alt: A voltage divider circuit built with a diode and resistor connected to a DC power source. (a) Diode schematic. (b)Forward biased diode. (b) Reverse biased diode.
A voltage divider circuit built with a diode and resistor connected to a DC power source. (a) Diode schematic. (b)Forward biased diode. (b) Reverse biased diode.
```

Part 2 of this lab is to use LabVIEW, a DAQ, function generator, and oscilloscope to automate the experiment.
Procedure

# Part 1 - Theory of P-N Junctions
For a semiconductor like silicon, the electrons fill the valence energy levels (band). There is a small energy gap $(E_g\approx1~{\rm eV})$  to the next levels, the conduction band. A 1D diagram of energy is shown in [](#fig:diodes:bandgaps).
```{figure} ../figures/ch6_diodes/bandgaps.svg
:label: fig:diodes:bandgaps
:width: 100%
:align: center
:alt: A band diagram of a metal, semiconductor, and insulator. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band.
A band diagram of a metal, semiconductor, and insulator. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band.
```
Metals have no energy gap between filled and unfilled energy bands and conduct readily. However, semiconductors with an energy gap an order of magnitude larger than the thermal energy ($E_g \ge 40 k_BT$ at room temperature), a very small fraction of electrons will be in the conduction band at room temperature. The statistics for populating the conduction band follow Boltzmann statistics.
```{math}
P=e^{-E_g/k_BT}
```
This gives about $P=10^{-17}$ at room temperature, and the density of silicon is about $10^{26}~{\rm atoms/cm^3}$. Therefore, there are about $10^9$ conduction electrons per cm<sup>3</sup>. However, if we dope the silicon with a small number of impurities, we can produce more conduction electrons. Suppose we add an element that has 5 outer shell electrons instead of silicon’s 4 electrons. The fifth electron will not participate in covalent bonding and is somewhat free to move around. Because the valence band is full, the fifth electrons must sit at a higher energy, closer to the conduction band. This shifts the Fermi Energy closer to the conduction band because the extra electrons are at an energy that is in the gap as shown in [](#fig:diodes:ndopedbands).
```{figure} ../figures/ch6_diodes/ndopedbands.svg
:label: fig:diodes:ndopedbands
:width: 100%
:align: center
:alt: A band diagram of an electron-doped semiconductor. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band. The electron-rich antimony donates somewhat free electrons. A very small amount of energy (comparable to thermal energy) pushes them up into conduction.
A band diagram of an electron-doped semiconductor. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band. The electron-rich antimony donates somewhat free electrons. A very small amount of energy (comparable to thermal energy) pushes them up into conduction.
```
The result is a density of conduction electrons equal to the density of doping, typically around $10^{16}~{\rm electrons/cm^3}$. The thermal energy easily promotes some of these electrons into the conduction band. The majority carrier is the electron. We call this an n-type material.

Alternatively, we could dope with electron deficient atoms such as boron with only 3 outermost electrons. This makes the covalent bonding short an electron, leaving a hole. See [](#fig:diodes:pdopedbands).
```{figure} ../figures/ch6_diodes/pdopedbands.svg
:label: fig:diodes:pdopedbands
:width: 100%
:align: center
:alt: A band diagram of a hole-doped semiconductor. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band. The electron-poor boron creates holes that would accept electrons. These holes form just above the valence band.
A band diagram of a hole-doped semiconductor. The Fermi Energy is defined to be halfway between the highest filled energy band and the next empty band. The electron-poor boron creates holes that would accept electrons. These holes form just above the valence band.
```
The electron vacancies fall just above the valence and shift the Fermi Energy close to the valence band. Electrons can easily “hop” to the acceptor holes with the available thermal energy. This can be thought of as holes falling into the valence band, which are then free to conduct along the valence band. The majority carrier is the hole. We call this a p-type material. Generally, electrons will fall to the lowest energy possible, while holes will then rise or float to higher energies.

Neither of these materials are particularly remarkable on its own. We essentially made a metal out of a semiconductor by doping. However, a revolution to the solid state electronics industry was the discovery of the p-n junction. When p-type and n-type materials are placed in contact with each other, the junction behaves very differently than either type of material alone. Specifically, current will flow readily in one direction (forward biased) but not in the other (reverse biased), creating the basic diode. This non-reversing behavior arises from the nature of the charge transport process in the two types of materials.

When p- and n-type materials are in contact, the bands will bend to keep the Fermi Energy constant across the junction. The result is that donor electrons in the n-type material are at an energy just below the energy of the acceptor holes in the p-type as shown in [](#fig:diodes:pnjunctionE).
```{figure} ../figures/ch6_diodes/pn_junction_energy.svg
:label: fig:diodes:pnjunctionE
:width: 60%
:align: center
:alt: A p-n junction has unique band behavior where the bands bend to keep the Fermi Energy constant across the junction. A pn-junction with depletion zone due to recombination of electrons and holes. The recombination and depletion leads to an electric field. The combination of no free charge carriers and the electric field makes the pn-junction have a very high resistance to current flow. 
A p-n junction has unique band behavior where the bands bend to keep the Fermi Energy constant across the junction. A pn-junction with depletion zone due to recombination of electrons and holes. The recombination and depletion leads to an electric field. The combination of no free charge carriers and the electric field makes the pn-junction have a very high resistance to current flow.
```
As you might imagine, the electrons and holes in the region near the interface can “recombine”. The electrons cannot move completely into the p-region because the conduction band is too high and similarly for the holes and the valence band. As electrons and holes recombine near the junction, they leave behind charged (ionized) atoms. The atoms are bound to the crystal lattice and cannot move freely. The result is a thin region at the junction where electrons and holes are no longer free. We call this the depletion zone because the region is depleted of free charge carriers. Furthermore, the ionized atoms create a potential difference across the depletion zone. This is shown in [](#fig:diodes:pnjunctionE). This figure is not to scale. In reality, the depletion zone is about 1/1000 of the width of the entire diode pn-junction.

To make the junction behave like a metal, we need to push the p-type bands down and push the n-type bands up. We can do this by applying a forward bias as shown in [](#fig:diodes:diodeVdivider) or [](#fig:diodes:pnjunctionbias). As the bias potential (voltage) increases, the bands become more and more aligned. Eventually, the bands align and the bias potential produces current flow that follows Ohm's Law (linear current vs. voltage).
```{figure} ../figures/ch6_diodes/pn_junction_bias.svg
:label: fig:diodes:pnjunctionbias
:width: 100%
:align: center
:alt: Biasing conditions of a pn-junction and the resulting band shifting. (a) reverse-biased, (b) unbiased, and (c) forward-biased diode.
Biasing conditions of a pn-junction and the resulting band shifting. (a) reverse-biased, (b) unbiased, and (c) forward-biased diode.
```
Reverse biasing ([](#fig:diodes:pnjunctionbias)(a)) pushes the bands in the opposite direction as forward biasing ([](#fig:diodes:pnjunctionbias)(c)), causing an increasingly insulating device. At high enough reverse bias, material will break down, and the diode is destroyed.

The current in a forward biased pn-junction can be modeled by the equation
```{math}
:label: eq:diodes:idealdiode
I = I_s \left(e^{V_d/nV_T}-1\right)
```
Where $I_s$ is the the magnitude of the current that flows for negative $V_d$ in excess of a few $V_T$, typically $10^{−12}~{\rm  A}$. The voltage across the diode is $V_d$. The value $n$ is the ideality of the diode, usually $1\le n\le3$. The value $V_T=k_BT/q$ is the thermal energy per charge carrier, around 26 mV at room temperature. [](#fig:diodes:idealdiode) shows this equation modeling zener diode data.
```{figure} ../figures/ch6_diodes/diodemodel.svg
:label: fig:diodes:idealdiode
:width: 100%
:align: center
:alt: Equation {eq}`eq:diodes:idealdiode modeling zener diode data.
Equation {eq}`eq:diodes:idealdiode modeling zener diode data.
```

# Part 1 - Measurements

This is a DC measurement. Set up the circuit as shown in [](#fig:diodes:diodeVdivider) for forward bias with a zener diode. Biasing is shown in [](#fig:diodes:pnjunctionbias). A voltage divider circuit built with a diode and resistor connected to a DC power source. (a) reverse-biased, (b) unbiased, and (c) forward-biased diode.

Using a zener diode, you will adjust $V_o$ and measure $V_R$ for a known resistor. Choose a resistor of about 100 Ω.
```{exercise}
Remind yourself starting from Ohm’s Law $V_o = V_d + V_R = IR_d + IR$ that the voltage divider circuit of [](#fig:diodes:diodeVdivider) allows you to calculate 

$$I=\frac{V_o - V_d}{R}=\frac{V_R}{R}$$
```
Collect data for the forward bias condition from 0 V to high enough voltage to see the exponential rise in current and with small enough steps to see the curvature. Set up the circuit for reverse bias and try to measure the point at which the reverse current is allowed to flow. A special design feature of zener diodes is to allow reverse current without breakdown. See [](#fig:diodes:zenerIV).
```{exercise}
* Plot your data for $I$ vs. $V_d$. Repeat the experiment with a silicon diode.
* Calculate the band gap by fitting the Ohmic region of positive diode current vs. voltage to a line. This will give the “turn-on” voltage, which is when the bias is equal to the band gap. Your result will look similar to [](#fig:diodes:diodefits). Example code is shown below to do this.
```
```{figure} ../figures/ch6_diodes/zener.svg
:label: fig:diodes:zenerIV
:width: 100%
:align: center
:alt: IV-curve of a zener diode.
IV-curve of a zener diode.
```
```{figure} ../figures/ch6_diodes/diodeIVfit.svg
:label: fig:diodes:diodefits
:width: 100%
:align: center
:alt: Graph of a silicon and 3.3 V zener diode. The forward voltage where current begins to pass can be found from fitting a line to the asymptotic end of the curve. The x-axis crossing is the “turn-on” voltage. The data in the graph results in 0.18 V for the silicon diode and 0.63 V for the zener diode. The silicon diode used to create this data must have been mislabeled. How can you tell?
Graph of a silicon and 3.3 V zener diode. The forward voltage where current begins to pass can be found from fitting a line to the asymptotic end of the curve. The x-axis crossing is the “turn-on” voltage. The data in the graph results in 0.18 V for the silicon diode and 0.63 V for the zener diode. The silicon diode used to create this data must have been mislabeled. How can you tell?
```
```{code-cell} python
# curve_fit optization
def f_line(x, a, b):
    return a*x + b

a = 0.01
b = -1

#Get zener fit
xtemp = zener_df['Vd'].loc[zener_df['Vd'] > 0.63]
ytemp = zener_df['I'].loc[zener_df['Vd'] > 0.63]
zener_params, zener_pcov = curve_fit(f_line, xtemp, ytemp, (a,b))

#Get silicon fit
xtemp = silicon_df['Vd'].loc[silicon_df['Vd'] > 0.199]
ytemp = silicon_df['I'].loc[silicon_df['Vd'] > 0.199]
silicon_params, silicon_pcov = curve_fit(f_line, xtemp, ytemp, (a,b))

#Print fit params
print(zener_params, zener_pcov)
print(silicon_params, silicon_pcov)

#Plot the results
xx = linspace(0,1, 200)
plt.plot(zener_df['Vd'], zener_df['I'], 'bo', label='zener')
plt.plot(xx, f_line(xx, *zener_params), '-b')
plt.plot(silicon_df['Vd'], silicon_df['I'], 'rs', label='silicon')
plt.plot(xx, f_line(xx, *silicon_params), '-r')
plt.hlines(0, 1, 0, linestyle='solid', color='black')
plt.legend(loc=0)
plt.grid(True)
plt.xlim(0, 1)
plt.ylim(-0.0001,0.005)
plt.xlabel('Diode Voltage (V)')
plt.ylabel('Diode Current (A)')
plt.savefig('diodeIVfit.svg')
plt.show()
```

# Part 2 - Other diode measurements (Choose 1)

## LED

You can measure LEDs. The color is an indication of the band gap, and using
```{math}
E_g=\frac{hc}{\lambda}
```
one can find the wavelength of emitted light using the linear fitting mentioned above. See [](#fig:diodes:diodeIVfit). In this equation, $h = 4.136\times10^{-15}~{\rm eV\cdot s}$ is Planck's constant. The speed of light is $c=3\times 10^8~{\rm m/s}$. Compare your wavelength to the portion of the visible spectrum for that color.
```{figure} ../figures/ch6_diodes/led_rainbow.svg
:label: fig:diodes:ledrainbow
:width: 50%
:align: center
:alt: LEDs can be obtained with gap energies across the infrared, visible, and ultraviolet electromagnetic spectrum.
LEDs can be obtained with gap energies across the infrared, visible, and ultraviolet electromagnetic spectrum.
```

## Rectifier Circuits
Rectifier circuits can be constructed with diodes. These circuits convert AC signals to *nearly* DC. A half wave rectifier converts only the positive portion of an AC input signal. The circuit diagram for a half wave rectifier is the same as the voltage divider except [](#fig:diodes:diodeVdivider) with an AC input voltage. A full wave rectifier converts both the positive and negative portions of an AC input signal. RC filtering can be added to smooth the diode rectification. In the case of RC filtering, one wants a low-pass filter. This is related to the value of RC. [](#fig:diodes:rectifiers) shows half, full, and filtered full wave rectifier circuits. Build each one using the following values and components.
:::{table} Rectifier circuit values and components
:label: table:diodes:rectifiers
:align: center

| input voltage | frequency | diode | load resistor |
| ------------- | --------- | ----------- | ------------- |
|     10 V sine |    60 Hz  |    1N4007   | 100 $\Omega$  |
:::
```{figure} ../figures/ch6_diodes/fullrectifier.svg
:label: fig:diodes:rectifiers
:width: 75%
:align: center
:alt: Filtered full wave rectifier circuit diagrams.
Filtered full wave rectifier circuit diagrams.
```

```{exercise}
* Try 5 and 50 $\mu$F capacitors for the filtering and describe and sketch how the capacitor value affects the output signal shape.
* How does the output voltage compare to the input voltage?
```
