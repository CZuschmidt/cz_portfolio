---
title: "FPGA-Based Digital Control of a Synchronous Buck Converter"
date: 2026-08-01
category: "Power Electronics"
summary: >-
  A 12 V to 5 V, 3 A synchronous buck converter regulated by a digital control
  loop written in Verilog on a Spartan-7 FPGA.
image: "/assets/img/projects/fpga-buck-converter/schematic.png"
image_alt: "LTspice schematic of a synchronous buck converter"
image_caption: "LTspice model of the synchronous buck power stage."
skills: ["LTspice", "Verilog", "Spartan-7 FPGA", "Power electronics", "Control systems"]
duration: "Aug 2026 – present (in progress)"
links:
  - label: "Source code"
    url: "https://github.com/CZuschmidt/FPGA-Buck-Converter"
---

## Overview

This project builds a synchronous buck converter whose voltage regulation is
handled digitally by an FPGA rather than by an analog controller IC.

## Specifications

| Parameter           | Value   |
| ------------------- | ------- |
| Input voltage       | 12 V    |
| Output voltage      | 5 V     |
| Output current      | 3 A     |
| Switching frequency | 150 kHz |

## Power stage

I defined the specifications above and am simulating the synchronous buck power
stage in LTspice. In the model, two NMOS switches (M1 high-side, M2 low-side) are
driven by separate PWM sources and feed an LC output filter (L1, C2) into the
load R1, with C1 as the input capacitor.

## Next: digital control loop

The next stage is a Verilog control loop on a Spartan-7 FPGA:

- PWM generation for the high- and low-side switches
- Dead-time insertion so the two switches never conduct at the same time
- ADC sampling synchronized to the switching cycle
- A digital compensator for closed-loop voltage regulation
