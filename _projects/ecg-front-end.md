---
title: "Wireless ECG Monitor"
date: 2026-10-01
order: 6
category: "Current class project · ESE 2150"
summary: >-
  A battery-powered ECG: a three-stage analog front end amplifies and filters
  the heart's millivolt signal, an nRF52840 Feather digitizes it, and
  Bluetooth sends it to a laptop to calculate heart rate.
image: "/assets/img/projects/ecg-front-end/signal-chain.svg"
image_alt: "Block diagram: electrodes feed an AD623 instrumentation amplifier, a 160 Hz low-pass stage with gain and a 0.5 Hz high-pass stage on a 3.3 V battery supply, then an nRF52840 Feather ADC that sends data over Bluetooth to a laptop for heart rate"
image_caption: "Signal chain of the ECG monitor (illustration)."
skills: ["Instrumentation amplifiers", "Op amps", "Analog filters", "nRF52840", "Bluetooth LE", "Python"]
role: "Current class project, ESE 2150 (Circuits and Systems)"
duration: "Oct 2026 – present"
---

## Overview

The heart's electrical activity reaches the skin as a signal of about a
millivolt, buried in noise. This ESE 2150 final project builds a complete ECG:
an analog front end that conditions the signal, a microcontroller that
digitizes it, and a wireless link that sends it to a laptop to calculate heart
rate.

## Analog front end

The circuit runs from a 3.7 V battery through the Feather's 3.3 V regulator,
which keeps it portable and isolated from mains power. A resistor divider sets
a mid-supply virtual ground so the op amps have room to swing on a single
supply.

- **Stage 1, AD623 instrumentation amplifier:** high gain on the difference
  between the electrodes, with low-frequency attenuation.
- **Stage 2, 160 Hz low-pass filter:** removes high-frequency noise, followed
  by a non-inverting gain stage on a TLV2462 rail-to-rail op amp.
- **Stage 3, 0.5 Hz high-pass filter:** removes baseline drift while keeping
  the slow parts of the PQRST wave.

The target is about 60 dB of gain overall. Each stage is built and verified on
its own with scope captures and Bode plots from 10 Hz to 1 kHz, then the full
chain is tested with a Contec ECG simulator at different heart rates and
amplitudes.

## Why an instrumentation amplifier

Lab 8 compared a resistor differential amplifier with an instrumentation
amplifier, using a 100 kΩ resistor in series with one input to model body
impedance.

- **Differential amplifier:** measured gain of 9.76 against a design of 10.
  With the body impedance added, the gain drops sharply and the resistor
  matching that gives common-mode rejection is lost.
- **Instrumentation amplifier:** measured gain of 10.55 against a design of 10,
  and unchanged with the 100 kΩ in place, because each input drives an op-amp
  buffer that draws almost no current.

## Digitizing and heart rate

- The nRF52840 Feather's ADC samples the front-end output, with its resolution
  and reference voltage chosen to fit the ECG signal's range.
- The Feather on the breadboard runs CircuitPython and sends samples over
  Bluetooth LE to a second Feather, which passes them to a laptop over USB.
- A Python script plots 20 pulses and calculates average heart rate from the
  time between R-peaks, with a median filter to help detect the peaks.
