---
title: Chapter 9 - Digital Integrated Circuits
kernelspec:
  name: python3
  display_name: 'Python 3'
---
(chap:digital)=
# Overview

:::{hint} Learning Objectives
* Students will demonstrate proficiency in the observation, analysis, and interpretation of experimental data, including the role that uncertainty plays in interpreting experimental results.
* Students operate signal generators and oscilloscopes to set up experiments with operational amplifiers.
* Students analyze data related to op amp circuits.
* Students articulate results of these experiments including experimental uncertainty.
:::

# Introduction

In this lab, you will use the 555 Timer to do fun things in a variety of modes that it can operate.[^1][^2] You will
* create a blinking light or timer. 
* create a trigger pulse
* control motors, create an alarm, create a musical instrument, and much more.

Let’s start with an overview of the pins.

### 555 Timer Pinout

**Pin 1 Ground**
This pin connects to the negative side of the battery.

**Pin 2 Trigger**
When this pin goes low (less than one-third of VCC), the output goes high.

**Pin 3 Output**
The output voltage from the chip is around 1.5 V lower than VCC when high and around 0 V when low. A 555 timer can give out only 100 to 200 mA in total. Check your chip’s datasheet for the exact value.

**Pin 4 Reset**
This pin resets the whole circuit. It’s an “inverted” pin, which means it resets when the pin goes low. This means the pin must be high normally so that the chip isn’t in a “reset” state.

**Pin 5 Control Voltage**
This pin is used to control the threshold voltage of the Threshold pin. This can be useful when you want to adjust the frequency of the circuit without changing the values of R1, R2, and C1. This pin should be connected with a capacitor (0.01 µF/10 nF) to ground; this is a way to keep any noise on it from influencing the frequency.

**Pin 6 Threshold**
This pin sets the output back to low when the voltage goes high (above two-thirds of VCC).

**Pin 7 Discharge**
This pin is unconnected when output is high, and it’s connected to ground when output is low.

**Pin 8 VCC Supply**
This is the positive power supply pin and can take a voltage between 5 and 15 V.
```{figure} ../figures/ch9_digital/555timerpinout.png
:label: fig:digital:555pinout
:width: 75%
:align: center
:alt: A pinout diagram of the 555-timer integrated circuit.
A pinout diagram of the 555-timer integrated circuit.
```

# Part 1 - Astable Mode

When the 555 Timer is in astable mode it means that the output will never be stable. The output will keep switching between `HIGH` and `LOW` forever. That means it works as an oscillator. You can use this to blink a light, create sound, control motors, and much more! A circuit diagram is shown in [](#fig:digital:555astable).
```{figure} ../figures/ch9_digital/555TimerAstableMode.png
:label: fig:digital:555astable
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer in astable mode.
A circuit diagram of the 555-timer in astable mode.
```

## 555 Timer Astable Circuit Example
Our first example is how to blink an LED with the 555 Timer. This is like the “hello world” equivalent of this IC.
Circuit components
* 555 Timer IC
* R1-R3: Resistor, 1 kΩ
* LED1: Red 5mm LED or similar
* C1: Capacitor, 1000 µF
* C2: Capacitor, 10 nF (it may work without this)

You don’t need exact values for the resistors and capacitors. But if you use the values listed above, your LED should blink about once every other second. Use the [555 Timer calculator](#https://www.build-electronic-circuits.com/circuit-calculator-conversion/555-timer-calculator/) to find the blinking frequency for other values.

# References

[^1]:https://www.build-electronic-circuits.com/555-timer/
[^2]:https://www.instructables.com/555-Timer/

