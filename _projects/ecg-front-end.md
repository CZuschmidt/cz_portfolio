---
title: "ECG Analog Front End"
date: 2026-09-15
order: 6
category: "Current class project · ESE 2150"
summary: >-
  An op-amp signal chain that amplifies and filters the heart's electrical
  signal from skin electrodes so the ECG waveform can be viewed on an
  oscilloscope.
image: "/assets/img/projects/ecg-front-end/signal-chain.svg"
image_alt: "Block diagram: electrodes feed an instrumentation amplifier, a high-pass filter, a low-pass filter and a gain stage, with the output going to an oscilloscope; an ECG trace runs above the chain"
image_caption: "Signal chain of the ECG front end (illustration)."
skills: ["Op amps", "Analog filters", "Circuit analysis", "Oscilloscope"]
role: "Current class project, ESE 2150 (Circuits and Systems)"
duration: "Fall 2026"
---

## Overview

The heart's electrical activity reaches the skin as a signal of about a
millivolt, buried in noise. This ESE 2150 project is an analog front end built
from op-amp stages that turns that signal into a clean waveform on an
oscilloscope.

## Signal chain

- **Instrumentation amplifier:** amplifies the difference between two
  electrodes while rejecting noise common to both, such as power-line
  interference.
- **High-pass filter:** removes the DC offset and slow baseline drift caused by
  electrode contact and movement.
- **Low-pass filter:** removes high-frequency noise above the band that carries
  the ECG.
- **Gain stage:** scales the filtered signal to a level that is easy to view
  and measure.

## Design approach

Gains and cutoff frequencies come from the course's circuit-analysis methods,
transfer functions and frequency response, and each stage is checked in
simulation and on the bench.
