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
```{figure} ../figures/ch7_transistors/BipolarTransistor3Dmodel.png
:label: fig/transistors/transistormodel
:width: 50%
:align: center
:alt: Model of a TO-92 package, commonly used for small bipolar transistors.
3D model of a TO-92 package, commonly used for small bipolar transistors. The pins from left to right when facing the flat side are specified by the manufacturer. [^1]
```
```{figure} ../figures/ch7_transistors/NPN_AND_PNP_BJT_SYMBOLS.png
:label: fig/transistors/transistorsymbols
:width: 75%
:align: center
:alt: The circuit diagram symbol of pnp and npn type bipolar junction transistor (bjt).
The circuit diagram symbol of pnp and npn type bipolar junction transistor (bjt). [^2]
```
```{figure} ../figures/ch7_transistors/NPN_BJT_Basic_Operation.svg
:label: fig/transistors/npnbasicoperation
:width: 100%
:align: center
:alt: An npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction.
An npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction. [^3]
```
```{figure} ../figures/ch7_transistors/NPN_BJT_Structure_n_circuit.svg
:label: fig/transistors/npncircuit
:width: 50%
:align: center
:alt: An alternative view of an npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction.
An alternative view of an npn bjt with forward biased b-e junction and reverse biased b-c junction.
NPN BJT with forward-biased B–E junction and reverse-biased B–C junction. [^4]
```
```{figure} ../figures/ch7_transistors/NPN_Band_Diagram_Equilibrium.svg
:label: fig/transistors/npnbandsequilibrium
:width: 80%
:align: center
:alt: Band diagram of an npn transistor in equilibrium (no bias). 
Band diagram of an npn transistor in equilibrium (no bias). [^5]
```
```{figure} ../figures/ch7_transistors/NPN_Band_Diagram_Active.svg
:label: fig/transistors/npnbandsactive
:width: 80%
:align: center
:alt: Band diagram for NPN transistor in active mode, showing injection of electrons from emitter to base, and their overshoot into the collector. 
Band diagram for NPN transistor in active mode, showing injection of electrons from emitter to base, and their overshoot into the collector. [^6]
```

[^1]: Image by Bazylevnik0 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=130428568
[^2]: Image by Osbert Joel for Electrical Classroom - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=106111550
[^3]: Image by Jp314159 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=78389923
[^4]: Image by Inductiveload - Own workBased on File:Npn-structure.png, by User:Heron at the English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=11068618
[^5]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696512
[^6]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696520