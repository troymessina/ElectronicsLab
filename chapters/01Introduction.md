---
title: Chapter 1 - Introduction
numbering:
  headings:
  heading_1:
    start: 1
---
(chap:introduction)=
## Introduction
Electronics play a crucial role in modern laboratories across all sciences — physics, chemistry, biology, and geology — enabling precise measurement of variables like temperature, light, magnetic fields, and more through common transducers. This course is a broad introduction to the electronic tools and techniques widely used today. Rather than making you an expert, this set of experimental activities aims to build your familiarity with practical devices like op amps, data acquisition, and specialized ICs. You'll also gain hands-on experience designing simple circuits and creating computer-controlled data systems. 
```{figure} ../figures/ch0_introduction/electronicsLabAI.png
:label: fig:intro:electronicslab
:width: 60%
:align: center
:alt: Electronics equipment (generated with Google Gemini AI).
```
There is also a portion of this book dedicated to using LabVIEW. LabVIEW is a program designed for electronic interfacing, experiment control, data acquisition, simulation and modeling. It is ubiquitous in science and engineering laboratories, both academic and commercial.

I've intentionally limited the amount of theory in this manual. I want this manual to serve as a modern-day tutorial, similar to the Radio Shack Workbooks of times past. The goal is to help you become more independent and confident in your learning and to make you proficient at the practice of electronics.

The experiments are written to take one or two 3-hour lab periods.

## Safety
Most of the electronics that will be practiced in this manual are no more dangerous than those one may encounter using typical electronic
devices such as cell phones.Many electronics textbooks do not even discuss safety hazards. Probably, the primary hazard in following this manual is mechanical rather than electrical, for example, dropping an instrument or computer on your foot. However, care and safety are always important, and one should avoid exceeding tolerances on all devices. Resistors can get very hot, very fast and can lead to skin burns if touched. Transistors are famous for “popping” when improperly wired. The minor explosion from one could damge the eye. Soldering will not be a significant component of this manual, but solder contains harmful heavy metals and caution should be exercised to protect eyes, hands, and lungs.

It is important not to take electronics lightly. In many lab settings, you'll encounter high voltages that can be dangerous — a current of just a few milliamperes through the heart can be life-threatening. When working with high voltage, it's wise to ground your arm to prevent current from passing through your body if contact is made.

Even when high voltage is not involved, using grounding straps is a good habit—not for your safety, but to protect sensitive electronic components from static discharge, which can easily damage semiconductors. While we don't have enough grounding straps for everyone, most components used in this course are inexpensive. However, if you're working with more advanced components, be sure to ask about borrowing a grounding strap.

## Measurement Instruments

### Multimeters
We will normally use handheld and benchtop instruments. We will use handheld digital multimeters (DMM) in this course. most likely the ExTech MN36 seen in [](#fig:intro:dmm). 
```{figure} ../figures/ch1_introduction/ExtechMN36.jpg
:label: fig:intro:dmm
:width: 60%
:align: center
:alt: ExTech MN36 digital multimeter.
ExTech MN36 digital multimeter.
```
The FeelTech FS3200 signal generator shown in [](#fig:intro:siggen) will be used to create time-dependent (AC) electronic signals.
```{figure} ../figures/ch3_oscopes/FeelTech.jpg
:label: fig:intro:siggen
:width: 60%
:align: center
:alt: The FeelTech FS3200 signal generator.
The FeelTech FS3200 signal generator.
```
The Tektronix 1102BEDU oscilloscope shown in [](#fig:intro:oscope) will be used to measure time-dependent (AC) electronic signals.
```{figure} ../figures/ch3_oscopes/Tektronix.jpg
:label: fig:intro:oscope
:width: 60%
:align: center
:alt: The Tektronix 1102BEDU oscilloscope.
The Tektronix 1102BEDU oscilloscope.
```

