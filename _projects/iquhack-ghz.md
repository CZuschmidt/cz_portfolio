---
title: "Quantum Entanglement Verification at MIT iQuHACK"
date: 2026-01-15
category: "Quantum Computing · Hackathon"
summary: >-
  Prepared a 20-qubit GHZ state in Qiskit and ran it on IQM superconducting
  cloud hardware during a 24-hour hackathon to verify multipartite entanglement.
image: "/assets/img/projects/iquhack-ghz/ghz-circuit.svg"
image_alt: "Quantum circuit diagram: a Hadamard gate on the first qubit followed by a chain of CNOT gates and a measurement on every qubit"
image_caption: "Structure of the GHZ-preparation circuit (illustration; 5 of the 20 qubits shown)."
skills: ["Qiskit", "Python", "Quantum circuits"]
role: "Hackathon participant"
duration: "24 hours, Jan 2026"
---

## Overview

At MIT iQuHACK I built a Qiskit circuit to prepare a 20-qubit
Greenberger–Horne–Zeilinger (GHZ) state and executed it on IQM superconducting
cloud hardware during the 24-hour hackathon.

## The circuit

A GHZ state puts every qubit into an equal superposition of all-zeros and
all-ones. The circuit creates it with a Hadamard gate on the first qubit,
followed by a chain of CNOT gates that spreads the entanglement to each of the
other qubits in turn.

## Verifying entanglement

I measured the output correlations across all qubits to verify multipartite
entanglement under real device noise.
