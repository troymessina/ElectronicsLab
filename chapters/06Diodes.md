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
```{figure} ../figures/ch6_diodes/pn_junction_energy.png
:label: fig:diodes:pnjunctionE
:width: 100%
:align: center
:alt: A p-n junction has unique band behavior where the bands bend to keep the Fermi Energy constant across the junction.
A p-n junction has unique band behavior where the bands bend to keep the Fermi Energy constant across the junction.
```
As you might imagine, the electrons and holes in the region near the interface can “recombine”. The electrons cannot move completely into the p-region because the conduction band is too high and similarly for the holes and the valence band. As electrons and holes recombine near the junction, they leave behind charged (ionized) atoms. The atoms are bound to the crystal lattice and cannot move freely. The result is a thin region at the junction where electrons and holes are no longer free. We call this the depletion zone because the region is depleted of free charge carriers. Furthermore, the ionized atoms create a potential difference across the depletion zone. This is shown in [](#fig:diodes:pnjunction).

```{figure} ../figures/ch6_diodes/pn_junction.svg
:label: fig:diodes:pnjunction
:width: 100%
:align: center
:alt: A pn-junction with depletion zone due to recombination of electrons and holes. The recombination and depletion leads to an electric field. The combination of no free charge carriers and the electric field makes the pn-junction have a very high resistance to current flow.
A pn-junction with depletion zone due to recombination of electrons and holes. The recombination and depletion leads to an electric field. The combination of no free charge carriers and the electric field makes the pn-junction have a very high resistance to current flow.
```

To make the junction behave like a metal, we need to push the p-type bands down and push the n-type bands up. We can do this by applying a forward bias as shown in [](#fig:diodes:diodeVdivider). The result is shown in [](#fig:diodes:pnjunctionbias)
. As the bias potential (voltage) increases, the bands become more and more aligned. Eventually, the bands align and the bias potential produces current flow.
```{figure} ../figures/ch6_diodes/pn_junction_bias.svg
:label: fig:diodes:pnjunctionbias
:width: 100%
:align: center
:alt: Biasing conditions of a pn-junction.
Biasing conditions of a pn-junction.
```
``````{figure}
:label: fig:diodes:pnjunctionbias
:width: 100%
:align: center
`````{grid}
:gutter: 3
````{grid-item}
```{image} ../figures/ch6_diodes/pnreversebias.svg
:alt: A pn-junction with a reverse bias.
:width: 80%
:align: center
```
````
````{grid-item}
```{image} ../figures/ch6_diodes/pnnobias.svg
:alt: A pn-junction with no bias.
:width: 80%
:align: center
```
````
````{grid-item}
```{image} ../figures/ch6_diodes/pnforwardbias.svg
:alt: A pn-junction with a forward bias.
:width: 80%
:align: center
```
````
`````
:alt: test 1, 2
 Testing a grid (a), (b), and (c).
``````
Reverse biasing (Fig. 7(c)) pushes the bands in the opposite direction as forward biasing, causing an increasingly insulating device. At high enough reverse bias, material will break down.

The current in a forward biased pn-junction can be modeled by the equation
```{math}
I = I_s \left(e^{V_d/nV_T}-1\right)
```
Where $I_s$ is the the magnitude of the current that flows for negative $V_d$ in excess of a few $V_T$, typically $10^{−12}~{\rm  A}$. The voltage across the diode is $V_d$. The value $n$ is the ideality of the diode, usually $1\le n\le3$. The value $V_T=k_BT/q$ is the thermal energy per charge carrier, around 26 mV at room temperature.

# Part 1 - Measurements

This is a DC measurement. Set up the circuit as shown in Figure 1 for forward bias with a zener diode. The figure is shown again in Figure 8.

Figure 8. A voltage divider circuit built with a diode and resistor connected to a DC power source. (a) Diode schematic. (b)Forward biased diode. (b) Reverse biased diode.

You will adjust Vin and measure VR for a known resistor. Choose a resistor of about 100-1000 Ω.
Deliverable 1: Remind yourself starting from Ohm’s Law Vin=Vd+ VR = IRdiode+IR that the voltage divider circuit of Figure 1 allows you to calculate 
Vd=Vin-VR 

I=Vin-VdR 
Collect data for the forward bias condition from 0 V to high enough voltage to see the exponential rise in current and with small enough steps to see the curvature. Set up the circuit for reverse bias and try to measure the point at which the reverse current is allowed to flow. A special design feature of zener diodes is to allow reverse current without breakdown. See Figure 9.
Deliverable 2: Plot data for I vs. Vd
Repeat the experiment with a silicon diode.
Deliverable 3: Calculate the band gap by fitting the asymptotic positive diode current vs. voltage to a line. This will give the “turn-on” voltage, which is when the bias is equal to the band gap.
```{figure} ../figures/ch6_diodes/zener.svg
:label: fig:diodes:zenerIV
:width: 100%
:align: center
:alt: IV-curve of a zener diode.
IV-curve of a zener diode.
```

Figure 10. Graph of a silicon and 3.3 V zener diode. The forward voltage where current begins to pass can be found from fitting a line to the asymptotic end of the curve. The x-axis crossing is the “on” voltage. The data in the graph results in 0.18 V for the silicon diode and 0.63 V for the zener diode. The silicon diode must have been mislabeled. How can you tell?
Other diode measurements (Choose 1)
LED
You can measure LEDs. The color is an indication of the band gap, and using

Egap=hc

one can find the wavelength of emitted light using the linear fitting mentioned above. See Figure 11.



Figure 11. Color dependence of LEDs. Red, yellow, green, and blue LEDs were measured to see how the band gap is tailored to create different emission wavelengths.
Photovoltaics
A solar cell is also a diode. When light shines on the cell, the donor (n-type) will have electrons excited into the conduction band. This leaves holes in the donor energy level. Near the junction, the holes will float upward to the p-type and electrons move deeper into the n-type due to the electric field in the depletion region. This results in a reverse current under illumination as shown in figure 12.

Figure 12. A PV cell IV curve in dark and under illumination.

Often, these IV curves are flipped over and the power vs. diode voltage are plotted to determine relevant parameters such as open circuit voltage and maximum power. See Figure 13. You are welcome to do an experiment to measure these values on a PV cell if you wish.



Figure 13. An IV and PV curve for a photovoltaic cell showing the various parameters of interest for these cells.
Diode Applications
Diodes are often used as protective elements. Silicon and germanium diodes, for example, offer one-way conductors such that a low forward bias voltage turns them on with low resistance. However, no current can flow backward for a reverse bias up to hundreds of volts.

Figure 11. Protective diode will not allow reverse current to flow.

Zener diodes are designed to have a low reverse bias turn-on. Zener diodes are often used in charging circuits because under a reverse bias, no current will flow through the diode as long as the load is not charged to the zener reverse turn-on voltage, i.e., the parallel load receives most of the current because the load is lower resistance. Once the load is charged, the voltage drop across the load and and zener will exceed the zener reverse turn-on voltage. At this point the load no longer receives current because the zener is a lower resistance path.

FIgure 12. A zener diode in reverse bias. Rload represents a rechargeable battery. The load resistance will be small while the battery charges from a low voltage to a charged voltage. Once the battery charges, the load resistance is large and the zener diode will become a low resistance path, cutting off charging current to the battery.
Rectifier circuits can also be constructed with diodes. Below are half and full wave rectifier circuits. See if you can explain why they produce the output they do.




A full wave rectifier can be smoothed by RC filtering.
