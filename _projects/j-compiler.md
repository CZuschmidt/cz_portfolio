---
title: "Compiler for the J Language"
date: 2026-10-01
order: 7
category: "Current class project · CIS 2400"
summary: >-
  A compiler written in C that translates programs in J, a small stack-based
  language, into RISC-V assembly.
image: "/assets/img/projects/j-compiler/pipeline.svg"
image_alt: "Pipeline diagram: program.j goes into a compiler written in C, made of a tokenizer and a code generator, which outputs program.s in RISC-V assembly"
image_caption: "Structure of the J compiler (illustration)."
skills: ["C", "RISC-V assembly", "Compilers", "Linux"]
role: "Current class project, CIS 2400 (Introduction to Computer Systems)"
duration: "Oct 2026 – present"
---

## Overview

For CIS 2400, this project is a compiler, written in C, that reads programs in
J, a small stack-based language, and translates them into RISC-V assembly that
can be assembled and run.

## How it works

- **Tokenizer:** reads the J source file and splits it into tokens: numbers,
  operators, keywords and function names.
- **Code generation:** for each token, the compiler emits RISC-V instructions
  that work on a stack in memory, pushing values and popping operands for
  arithmetic and comparisons.
- **Control flow:** conditionals and loops become labels and branch
  instructions.
- **Functions:** J functions compile to RISC-V functions that follow the
  standard calling convention, saving and restoring registers on the stack.

## Why it matters

Writing a compiler at this level means managing memory, the stack and
registers directly, and shows how C code maps to the instructions the
processor actually runs.
