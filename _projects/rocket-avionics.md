---
title: "Rocket Avionics and Flight Computer"
date: 2025-09-01
order: 2
category: "Rocketry · Avionics"
summary: >-
  Leading avionics for the Penn High-Power Rocketry team's competition rocket:
  a custom flight computer, attitude estimation, and the recovery and airbrake
  electronics.
image: "/assets/img/projects/rocket-avionics/competition.jpg"
image_alt: "Team members working on the rocket's avionics bay at night under a headlamp"
image_caption: "Working on the rocket's avionics at competition."
skills: ["STM32", "Altium", "KiCad", "PCB design", "RTOS firmware", "Kalman filtering", "Sensor fusion"]
role: "Avionics Project Lead"
team: "Penn High-Power Rocketry Team (IREC)"
duration: "Sep 2025 – present"
---

## Overview

I lead avionics for the Penn High-Power Rocketry team's rocket for the
Intercollegiate Rocket Engineering Competition (IREC). The work covers the
rocket's custom flight computer, its attitude-estimation software, and the
avionics bay that handles recovery and airbrake control.

## Flight computer

I am designing a custom STM32-based flight computer PCB in Altium and KiCad. It
combines IMU fusion, magnetometers, a barometer, a radio, GPS and flash logging,
and runs RTOS firmware.

{% include figure.html src="/assets/img/projects/rocket-avionics/flight-computer-render.jpg" alt="3D render of the flight computer circuit board with a microcontroller module, radio module and two SMA antenna connectors" caption="3D render of the flight computer PCB." %}

{% include figure.html src="/assets/img/projects/rocket-avionics/flight-computer-layout.jpg" alt="Top-down PCB layout in KiCad showing regulators, passives, a battery footprint and a 40-pin header" caption="Flight computer PCB layout in KiCad." %}

## Attitude estimation

The flight software implements a Multiplicative Extended Kalman Filter (MEKF)
for quaternion attitude estimation. It fuses gyroscope and accelerometer data,
weighting each sensor by the inverse of its variance.

## Avionics bay

I integrated a dual-deploy avionics bay with commercial altimeters, GPS and
ejection charges, and the avionics drive the control and actuation of the
rocket's airbrake system.

{% include figure.html src="/assets/img/projects/rocket-avionics/avionics-bay.jpg" alt="The rocket's avionics sled with circuit boards and wiring, laid out on a table" caption="The avionics bay at competition." %}
