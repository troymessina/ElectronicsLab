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

# Theory of Bipolar Junction Transistors

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
A bipolar junction transistor (BJT) is made up of three layers of semiconductor material, each with different electrical properties. These layers are called the emitter, base, and collector. In a PNP transistor, the order is p-type, n-type, then p-type. In an NPN transistor, it’s n-type, p-type, then n-type. Each layer is connected to a terminal with the same name: emitter (E), base (B), and collector (C).

The base is a very thin and lightly doped layer placed between the emitter and collector. The emitter sends charge carriers (like electrons or holes) into the base, and most of those carriers get collected by the collector. Because of how the transistor is designed—especially the fact that the collector surrounds the emitter—very few of the charge carriers escape. This makes the transistor very efficient at amplifying current, giving it a high current gain. A cross-sectional of an npn BJT is shown in [](#fig:transistors:npncrosssection).
```{figure} ../figures/ch7_transistors/NPN_BJT_Cross-section.svg
:label: fig/transistors/npncrosssection
:width: 75%
:align: center
:alt: A cross-section of the npn type bipolar junction transistor (bjt) collector-emitter-base structure.
A cross-section of the npn type bipolar junction transistor (bjt) collector-emitter-base structure. [^3]
```

One important thing to know about BJTs is that they are not symmetrical. This means you can't just flip the emitter and collector and expect it to work the same way. If you try to swap them, the transistor goes into what's called reverse mode, where it works much less effectively. This is because the emitter is heavily doped to push a lot of carriers into the base, while the collector is lightly doped to handle high voltages. The collector–base junction is normally reverse biased (it blocks current), and the emitter–base junction is forward biased (it allows current flow). The way the transistor is built makes sure that most of the current comes from the emitter, which is important for good performance. Performance is determined by a gain parameter, $\alpha$, and a figure of merit, $\beta$.

Beta ($\beta$) is a useful number that helps describe how well a bipolar junction transistor (BJT) can amplify current. However, it's not a basic physical constant. It's more like a helpful shortcut for understanding how the transistor behaves. Technically, BJTs are controlled by voltage, not current. The current flowing from the collector is mainly determined by the voltage between the base and the emitter. The current going into the base happens because of how the base–emitter junction is built, and it can be thought of as an unwanted side effect.

In many circuit designs, engineers assume that beta is large enough that the base current doesn’t significantly affect the circuit’s performance. In other cases, especially in switching circuits (where the transistor is just turned fully on or off), the base current is made large enough to ensure the transistor works properly, even if the transistor has a lower-than-expected beta.
```{math}
\alpha_F = \frac{I_C}{I_E} = \frac{\beta_F}{1+\beta_F}
```
```{math}
\beta_F = \frac{I_C}{I_B} = \frac{\alpha_F}{1-\alpha_F}
```
## Active Mode

In forward-active or active mode, the base–emitter junction is forward biased and the base–collector junction is reverse biased. Most bipolar transistors are designed to provide the greatest common-emitter current gain, $\beta_F$, in forward-active mode. If this is the case, the collector–emitter current is approximately proportional to the base current, but many times larger, for small base current variations.

[](#fig:transistors:npnbasicoperation) and [](#fig:transistors:npncircuit) show a circuit diagram of an npn transistor connected to two power sources. The applied voltage at the base causes the base-emitter pn-junction to become forward biased, allowing a flow of electrons from the emitter into the base (current from base to emitter). The reverse bias between the collector and base, the electric field existing between base and collector (caused by $V_{CE}$) will cause the majority of these electrons to cross the upper pn-junction into the collector to form the collector current $I_C$. The remainder of the electrons recombine with holes, the majority carriers in the base, making a current through the base connection to form the base current, $I_B$. As shown in [](#fig:transistors:npnbasicoperation) and [](#fig:transistors:npncircuit), the emitter current, $I_E$, is the total transistor current, which is the sum of the other terminal currents, (i.e. $I_E = I_B + I_C$).

[](#fig:transistors:npnbasicoperation) and [](#fig:transistors:npncircuit) indicate the traditional current with the arrows. The flow of electrons would be in the opposite direction of these arrows because electrons carry negative electric charge. In active mode, the ratio of the collector current to the base current is called the DC current gain $\beta_F$. This gain is usually 100 or more, but robust circuit designs do not depend on the exact value (for example see [](#chap:opamps). The value of this gain for DC signals is referred to as $h_{FE}$. When there are small changes in currents, the value of this gain is referred to as $h_{fe}$. In other words, under a steady state condition
```{math}
h_{FE}  = \frac{I_C}{I_B}
```
```{math}
h_{fe}  = \frac{\Delta I_C}{\Delta I_B}
```
$\beta$ is used interchangably for both $h_{FE}$ and $h_{fe}$
The emitter current is related to $V_{BE} exponentially. At room temperature, an increase in $V_{BE} by approximately 60 mV increases the emitter current by a factor of 10. Because the base current is approximately proportional to the collector and emitter currents, they vary in the same way.
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

## Band Theory

BJTs can be thought of as two diodes (pn-junctions) sharing a common region that minority carriers can move through. The npn transistor is as if two diodes were sharing a P-type anode region. Connecting two diodes with wires will not make a BJT, since minority carriers will not be able to get from one pn-junction to the other through the wire.

BJT function by letting a small current input to the base control an amplified output from the collector. This current occurs from a voltage bias on the base that lowers the energy of the p-type base. The lower the base energy is the more current that can flow from collector to emitter in the active mode. The result is that the BJT makes a good switch that is controlled by its base input turning on or off the current from collector to emitter. The BJT also makes a good amplifier, since it can multiply a weak base input signal to about 100 times its original strength with the addition of the current-emitter current. BJTs can be networked to build powerful amplifiers for many applications. A band diagram of an npn transitor is shown in [](#fig:transistors/npnbasicoperation) and [](#fig:transistors:npncircuit).
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
# Experiments

## Part 1 - The Transistor Switch


[^1]: Image by Bazylevnik0 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=130428568
[^2]: Image by Osbert Joel for Electrical Classroom - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=106111550
[^3]: Image by Inductiveload - Own work, Public Domain, https://commons.wikimedia.org/w/index.php?curid=11068760
[^4]: Image by Jp314159 - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=78389923
[^5]: Image by Inductiveload - Own workBased on File:Npn-structure.png, by User:Heron at the English Wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=11068618
[^6]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696512
[^7]: Image by Inductiveload - Own drawing, done in Inkscape, Public Domain, https://commons.wikimedia.org/w/index.php?curid=1696520