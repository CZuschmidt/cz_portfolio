---
title: "Compiler for the J Language"
date: 2026-10-01
order: 7
category: "Current class project · CIS 2400"
summary: >-
  jc, a compiler written in C that translates J, a stack-based language
  inspired by Forth, into RISC-V assembly that follows the clang calling
  convention.
image: "/assets/img/projects/j-compiler/pipeline.svg"
image_alt: "Pipeline diagram: source.j goes into jc, a compiler written in C made of a tokenizer and a code generator, which outputs source.s in RISC-V assembly to run in PennSim"
image_caption: "Structure of the J compiler (illustration)."
skills: ["C", "RISC-V assembly", "Compilers", "Makefiles", "Valgrind", "Linux"]
role: "Current class project, CIS 2400 (Introduction to Computer Systems)"
duration: "Oct 2026 – present"
---

## Overview

For CIS 2400, `jc` compiles programs written in J, a stack-oriented language
loosely inspired by Forth, into RISC-V assembly. Running `./jc source.j` writes
`source.s`, which is assembled and run in the PennSim simulator. Like clang,
`jc` only generates assembly; it never executes it.

## The J language

Every value in J is a 32-bit integer on a stack, and programs are written in
Reverse Polish Notation. `7 5 4 + *` pushes 7, 5 and 4, adds the top two and
then multiplies, leaving 63.

- **Literals:** decimal and hexadecimal (`0xD6DEF00D`), any 32-bit value
- **Arithmetic:** `+ - * / %`
- **Comparisons:** `lt le eq ge gt`, which push 1 or 0
- **Bitwise logic:** `and or not`
- **Stack operations:** `drop dup swap rot`
- **Control flow:** `if … else … endif` and `while … endwhile`, nested freely
- **Functions:** `defun name … return`, with `get_argN` and `set_argN` for
  arguments in `a0` to `a7`

```
defun square
get_arg1
dup *
return
```

## How jc works

- **Tokenizer (`token.c`):** `next_token` reads the source one token at a
  time, skipping whitespace and `;` comments, and classifies each token.
- **Code generation:** for each token, the compiler emits RISC-V instructions
  that push to and pop from a stack in memory. Constants too large for a
  12-bit immediate are built from an upper and a lower part.
- **Control flow:** every `if` and `while` gets unique labels, and a stack of
  open blocks tracks nesting so each `else`, `endif` and `endwhile` branches
  to the right place.
- **Functions:** prologues and epilogues follow the clang-19 calling
  convention, with `fp` (x8) and `sp` (x2), so J and C functions can call each
  other. After a call, the return value is pushed onto the J stack.

## Build and testing

The code is split across `token.c`, `jc.c` and a code-generation module, built
by a Makefile with clang-19 and `-Wall`. It is tested against sample J programs
in PennSim, checked for memory leaks with Valgrind, and graded by an
autograder and a verbal assessment.
