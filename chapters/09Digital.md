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
```{figure} ../figures/ch9_digital/555timerpinout.svg
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

**Circuit components**
* 555 Timer IC
* R1-R3: Resistor, 1 kΩ
* LED1: Red 5mm LED or similar
* C1: Capacitor, 1000 µF
* C2: Capacitor, 10 nF (it may work without this)

You don’t need exact values for the resistors and capacitors. But if you use the values listed above, your LED should blink about once every other second. Your circuit should be set up as shown in [](#fig:digital:555astableblink)
```{figure} ../figures/ch9_digital/555TimerAstableBlinkingLED.png
:label: fig:digital:555astableblink
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer in astable mode.
A circuit diagram of the 555-timer in astable mode.
```
Use the [555 Timer calculator](https://www.build-electronic-circuits.com/circuit-calculator-conversion/555-timer-calculator/) to find the blinking frequency for other values. Try it out!

# Part 2 - Monostable Mode

Monostable means the output is stable in one state, and it will always come back to this state. You can push it out of that state, but it will always return back to its stable state after a certain time. The output from the 555 Timer in monostable mode is normally LOW. When you trigger the circuit, the output goes HIGH for a certain amount of time before it goes back to LOW again. This is sometimes called a one-shot circuit. The time it stays HIGH is decided by the size of a resistor $R_1$ and a capacitor $C_1$. The higher the values, the longer it stays HIGH. If you connect a buzzer to the output, you can create an alarm circuit that is triggered for example by a window being opened. The monostable circuit diagram is shown in [](#fig:digital:555timermonostable)
```{figure} ../figures/ch9_digital/555TimerMonostableMode.png
:label: fig:digital:555monostable
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer in astable mode.
A circuit diagram of the 555-timer in astable mode.
```

## 555 Timer Monostable Circuit Example
The circuit shown in [](#fig:digital:555monostableLED) turns on an LED when you push the button. After about 10 seconds, the LED turns off.

**Circuit Components**
* 555 Timer IC
* R1: Resistor, 100 kΩ
* R2: Resistor, 5kΩ to 1 MΩ (this is a pull-up resistor)
* R3: Resistor, 1 kΩ
* LED1: Red 5mm LED or similar
* C1: Capacitor, 100 µF
* C2: Capacitor, 10 nF
* S1: Pushbutton, normally open

For longer delays, increase C1 and/or R1. If you want an adjustable delay, replace R1 with a potentiometer. Use the 555 Timer calculator to find the values you need.
```{figure} ../figures/ch9_digital/555TimerMonostableLED.png
:label: fig:digital:555monostableLED
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer in monostable mode.
A circuit diagram of the 555-timer in monostable mode.
```
The output is connected to control an LED, but could easily be modified to control a motor, a lamp, a coffee maker, or anything else. Just replace R3 and the LED with a transistor. See how in the section Driving Higher Loads below.

# Part 3 - Bistable Mode

Bistable, sometimes called "flip-flop", means the output is stable in both states (HIGH and LOW). It will stay in one state until you push it over to the other state. Then it stays in the other state. You push it from one state to the other with the Trigger and Threshold pins. This mode isn’t a timer function at all, and it’s not a common way to use the 555 Timer. In this mode, the 555 Timer works as a flip-flop. You can for example use it to reverse the direction of a robot when it bumps into a wall.

## 555 Timer Bistable Circuit Example

[](#fig:digital:555bistable) shows the 555 Timer in bistable mode. Here you have separate ON and OFF buttons to control an LED.
```{figure} ../figures/ch9_digital/555BistableExampleON-OFF.png
:label: fig:digital:555bistable
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer in bistable mode.
A circuit diagram of the 555-timer in bistable mode.
```
**Component List**
* 555 Timer IC
* S1, S2: Pushbutton, normally open
* R1, R2: Resistor, 5kΩ to 1 MΩ (these are pullup resistors)
* Resistor (R3): 1 kΩ
* LED: Red 5mm LED or similar
* Capacitor (C1): 10 nF

The output is connected to control an LED, but could easily be modified to control a motor, a lamp, or anything else by connecting a transistor. See [](#sec:digital:highloads) for examples.

(sec:digital:highloads)=
# Part 4 - Driving Higher Loads

If you want to control motors, LED strips, or other things that need more than 200 mA of current, you can connect a transistor to the output. If you want to use an npn transistor, you will need to connect a resistor between the output and the base to limit the base current. 1 kΩ will probably work fine as a starting point.
```{figure} ../figures/ch9_digital/555TimerBJTTransistorDriver.png
:label: fig:digital:555timerhighloads
:width: 75%
:align: center
:alt: A circuit diagram of the 555-timer set up for driving high loads in bistable mode.
A circuit diagram of the 555-timer set up for driving high loads in bistable mode.
```

# References

[^1]:https://www.build-electronic-circuits.com/555-timer/
[^2]:https://www.instructables.com/555-Timer/

