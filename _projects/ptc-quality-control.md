---
title: "Quality Control of the DUNE Power and Timing Card"
date: 2026-05-15
order: 1
category: "Research · Hardware Verification"
summary: >-
  Production quality-control testing of the Power and Timing Card (PTC), a
  Penn-designed board that powers and clocks the readout electronics of the
  DUNE neutrino detector.
image: "/assets/img/projects/ptc-quality-control/cover.jpg"
image_alt: "Power and Timing Card circuit board on the bench"
image_caption: "A production Power and Timing Card (board 009)."
skills: ["Hardware verification", "Python", "I²C", "Zynq UltraScale+", "PetaLinux", "EtherCAT", "TwinCAT", "Oscilloscope"]
role: "Undergraduate Researcher, Hardware Verification"
team: "Penn Instrumentation Group, High-Energy Physics"
duration: "May 2026 – present"
links:
  - label: "Research poster (PDF)"
    url: ""                      # export the poster from PowerPoint as PDF, upload it to assets/files/, then e.g. "/assets/files/ptc-qc-poster.pdf"
---

## Overview

The Deep Underground Neutrino Experiment (DUNE) sends a high-intensity neutrino
beam 1,300 km from Fermilab to the Sanford Underground Research Facility, where
liquid-argon detectors image the tracks left when neutrinos strike nuclei.
Inside the detector's readout electronics, up to six Warm Interface Boards
(WIBs) digitize detector data in each Warm Electronics Interface Crate, and each
crate is powered and clocked by one of 250 Power and Timing Cards.

As an undergraduate researcher in Penn's High-Energy Physics instrumentation
group, I perform production quality-control (QC) testing of the PTC, with the
goal of validating all 250 production boards before they are deployed.

## The Power and Timing Card

The PTC distributes regulated 12 V power and synchronized 62.5 MHz timing to the
WIBs. It is built around an Enclustra Mercury XU5 Zynq UltraScale+
system-on-module, which gives the board an embedded ARM processor and an FPGA.
The card:

- Enables, disables and controls power to each WIB channel
- Continuously monitors voltages and currents over I²C for fault detection
- Relays precise timing signals for data transfer
- Runs embedded Linux, built with PetaLinux, for on-board control and testing
- Connects to the detector safety system over EtherCAT (XMC4300
  microcontroller) and to the slow-control system over Gigabit Ethernet

{% include figure.html src="/assets/img/projects/ptc-quality-control/board-layout.jpg" alt="PTC board with regions outlined: 12 V regulators and sensors, auxiliary supplies, timing and network interfaces, system-on-module, and the WIB power connector" caption="PTC board layout: 12 V regulators with power and temperature sensors, auxiliary supplies, timing/EtherCAT/Gigabit Ethernet, the system-on-module, and the 12 V/I²C connector to the WIBs." %}

## QC test stand

The QC board stands in for a full crate. It emulates six WIBs and loads each of
the PTC's 12 V DC-DC converters through a PWM-controlled current sink. FPGA
register writes step each converter from about 1.5 A to about 6 A:

```
// write command, register address, PWM value
poke 0x8002004c 0x316
poke 0x8002004c 0x226
```

The QC board also hosts power and temperature sensors that the PTC reads through
an I²C multiplexer, feeding data back as a live WIB would, and it runs embedded
Linux on its own system-on-module. A test PC talks to the PTC over SSH/UART, and
a Beckhoff CX8110 PLC exercises the EtherCAT link.

{% include figure.html src="/assets/img/projects/ptc-quality-control/test-setup.jpg" alt="Test bench with the PTC, QC board, timing card and Beckhoff PLC, next to a block diagram of how they connect" caption="QC setup for full PTC testing, and how the test PC, CX8110 PLC, PTC, QC board and WIB interfaces connect." %}

## Testing, scripting and debugging

**Hardware.** Physical and analog checks with a digital voltmeter and an
oscilloscope: DC-DC load tests driving each converter to its full ~6 A, voltage
ripple and test-point validation, and visual inspection of part assembly and
orientation.

**Software.** A Python test package that reads every power and temperature
sensor over I²C, runs EEPROM, Gigabit Ethernet throughput and EtherCAT tests,
and sends results through a WebSocket client/server architecture to the lab's
hardware database.

**Firmware.** Building and loading what the system-on-module boots: the Vivado
FPGA bitstream and PetaLinux boot image, timing lock and setup, and programming
the XMC4300 microcontroller. I also configure the Beckhoff CX8110 EtherCAT master
in TwinCAT and decode EtherCAT process data during verification.

{% include figure.html src="/assets/img/projects/ptc-quality-control/ripple.jpg" alt="Oscilloscope capture showing the load-connected signal in yellow and the converter output ripple in cyan" caption="Example oscilloscope ripple measurement: load connected (yellow) and output ripple (cyan)." %}

A large part of the work is debugging. One example was tracing I²C
communication failures through the board's MAX7357 multiplexer trees to its
LTC2945 power and temperature monitors, using a microscope to inspect the
multiplexer on the QC board.

{% include figure.html src="/assets/img/projects/ptc-quality-control/microscope-debug.jpg" alt="Digital microscope positioned over the QC board, with a multimeter on the bench" caption="Microscope inspection while debugging the I²C multiplexer on the QC board." %}

## Results

- Refined and validated a QC test stand and procedure for the PTC covering power
  delivery, timing distribution, sensors, and the EtherCAT and Gigabit Ethernet
  interfaces, with defined acceptance criteria
- Exercised the procedure on prototype boards, helping establish a repeatable
  process for production testing
- Contributed to the lab's automated board-QC pipeline and wrote technical
  documentation of the PTC architecture and DUNE readout chain
- Presented the work as a research poster

## Next steps

- Integrate the automated Python test suite with a test UI
- Automate EtherCAT PLC testing with the PyADS library
- Test the next batch of 90 PTC boards to be sent to Fermilab

## Acknowledgements

This work was supported by the Penn Undergraduate Research Mentoring program
(PURM). Thank you to my advisors Adrian Nikolica and Elliot Lipeles, to David
Drobner, and to the other members of the Penn HEP group.
