---
title: Chapter 7 - Transistors
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:transistors)=
# Overview
:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments with transistors.
* Students analyze data related to transistor circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction
In this lab, you will explore transistor circuits. A very brief theory is given below. Much more detail can be found in this [Wikipedia article](#https://en.wikipedia.org/wiki/Bipolar_junction_transistor#NPN). You will build circuits to observe the transistor as a switch and as an amplifier.

# Theoretical 

The transistor is two pn-junctions. They can be npn or pnp. Arguably, the more common is the npn because of higher charge mobility, faster switching, and higher versatility. Because the transistor has three semiconductor regions, there are three electrical connections. A model of a typical transistor package, the TO-92, is shown in [](#fig:transistors:transistormodel).
```{figure} ../figures/ch7_transistors/BipolarTransistor3Dmodel.png
:label: fig/transistors/transistormodel
:width: 50%
:align: center
:alt: Model of a TO-92 package, commonly used for small bipolar transistors.
3D model of a TO-92 package, commonly used for small bipolar transistors. The pins from left to right when facing the flat side are specified by the manufacturer. [^1]
```
Circuits with transistors use the circuit diagram symbols shown in [](#fig:transistors:transistorsymbols). We will focus on the npn transistor, but the information presented for npn is similar for pnp transistors, which can to some extent be consider "opposite" to npn transistors. Transistors are considered directional as seen by the diode symbol in [](#fig:transistors:transistorsymbols) that connects the base to the emitter.
```{figure} ../figures/ch7_transistors/NPN_AND_PNP_BJT_SYMBOLS.png
:label: fig/transistors/transistorsymbols
:width: 75%
:align: center
:alt: The circuit diagram symbol of pnp and npn type bipolar junction transistor (bjt).
The circuit diagram symbol of pnp and npn type bipolar junction transistor (bjt). [^2]
```
A bipolar junction transistor's (BJT) three distinct semiconductor regions have different doping levels: the emitter, base, and collector. In a PNP transistor, these regions are p-type, n-type, and p-type, respectively; in an NPN transistor, the order is n-type, p-type, and n-type. Each of these regions is linked to a terminal identified as the emitter (E), base (B), or collector (C).

The base is positioned between the emitter and the collector and is constructed from a lightly doped material with high electrical resistance. The collector is designed to surround the emitter region, which helps ensure that most charge carriers introduced into the base are collected rather than lost. This design feature results in a current gain factor, $\alpha$, that is nearly one, thereby yielding a high $\beta$ value for the transistor.These values are defined by ratios of currents and are dependent on one another due to both depending on the collector current.
```{math}
\alpha_f = \frac{I_c}{I_e} = \frac{\beta_f}{1+\beta_f}
```
```{math}
\beta_f = \frac{I_c}{I_b} = \frac{\alpha_f}{1\alpha_f}
```
Structurally, the collector–base junction typically has a greater area than the emitter–base junction, as seen in cross-sectional views of BJTs shown in [](#fig:transistors:npncrosssection).
```{figure} ../figures/ch7_transistors/NPN_BJT_Cross-section.svg
:label: fig/transistors/npncrosssection
:width: 75%
:align: center
:alt: A cross-section of the npn type bipolar junction transistor (bjt) collector-emitter-base structure.
A cross-section of the npn type bipolar junction transistor (bjt) collector-emitter-base structure. [^3]
```

Unlike many other types of transistors, BJTs are generally not symmetrical. If the emitter and collector are swapped, the device no longer operates in its intended forward active mode but instead enters a reverse mode. In this reversed configuration, the current gain is significantly reduced, with α often falling below 0.5. This asymmetry is mainly due to differences in doping: the emitter is heavily doped to maximize carrier injection efficiency, while the collector is lightly doped to handle higher reverse bias voltages without breaking down. In standard operation, the collector–base junction is reverse biased. The heavy doping of the emitter ensures that the majority of charge carriers in the emitter–base junction are injected from the emitter side, which is essential for achieving a high current gain.


```{figure} ../figures/ch7_transistors/NPN_BJT_Basic_Operation.svg
:label: fig/transistors/npnbasicoperation
:width: 100%
:align: center
:alt: An npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction.
An npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction. [^4]
```
```{figure} ../figures/ch7_transistors/NPN_BJT_Structure_n_circuit.svg
:label: fig/transistors/npncircuit
:width: 50%
:align: center
:alt: An alternative view of an npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction.
An alternative view of an npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction. [^5]
```
```{figure} ../figures/ch7_transistors/NPN_Band_Diagram_Equilibrium.svg
:label: fig/transistors/npnbandsequilibrium
:width: 80%
:align: center
:alt: Band diagram of an npn transistor in equilibrium (no bias). 
Band diagram of an npn transistor in equilibrium (no bias). [^6]
```
```{figure} ../figures/ch7_transistors/NPN_Band_Diagram_Active.svg
:label: fig/transistors/npnbandsactive
:width: 80%
:align: center
:alt: Band diagram for NPN transistor in active mode, showing injection of electrons from emitter to base, and their overshoot into the collector. 
Band diagram for NPN transistor in active mode, showing injection of electrons from emitter to base, and their overshoot into the collector. [^7]
```

[^1]: Image by Bazylevnik0 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=130428568
[^2]: Image by Osbert Joel for Electrical Classroom - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=106111550
[^3]: Image by Inductiveload - Own work, Public Domain, https://commons.wikimedia.org/w/index.php?curid=11068760
[^4]: Image by Jp314159 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=78389923
[^5]: Image by Inductiveload - Own workBased on File:Npn-structure.png, by User:Heron at the English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=11068618
[^6]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696512
[^7]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696520