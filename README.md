# Lab 2: Introduction to SystemVerilog

## Before You Start
Depending on when your lab section is, you might not have gone over any verilog in lecture yet. Before you start this lab, you should go through the `BACKGROUND.md` in this repo. It will quickly go over everything you need to complete this lab.

Additionally, you do not need to clone this repository. You only need to clone the lab-common submodule.

## Ex 2.1: Setting up your environment

Initialize your submodule and move me in there.

Breakdown of the directory:
- `src/` --- where you find top.sv (your solution)
- `tb/`  --- where you implement your testbench. (make sure to name the simulation file `top_tb.sv`
- `build/` --- where all generated files go including the synthesized design (top.bit) and any generated waveforms
- `Makefile` --- Use this to build & simulate your project

## Ex 2.2: BCD-to-7SEG Decoder (Simulation only)

Yall don't have your kits yet. We're doing simulation this week... you get to synthesize the design on your FPGAs next week.

### System Input
```systemverilog
input wire [3:0] bcd
```
### System Output
```systemverilog
output logic [6:0] seg7
```

### Behavior

A BCD to 7-segment decoder converts a 4-bit Binary-Coded Decimal (BCD) input into signals needed to drive a 7-segment display. The input can be anything from `0b0000` to `0b1111`. The decoder will activate specific segment outputs (a–g) to correctly display the decimal digits 0 - 9 (for values between 0 and 9) or A - F (for values beteween 10 and 15). Each segment output is determined by combinational logic based on the input bits. The Verilog implementation should operate purely as combinational logic with no memory or clock dependency.

> Please use Background.md for supplemental information.

## Ex 2.3: Simulate the results

Flush out a testbench that iterates through the following test cases:
1. set bcd to 4'd0. show the resulting waveform?
1. set bcd to 4'd1. show the resulting waveform?
1. ...
1. set bcd to 4'd15. show the resulting waveform?

![ALt Text](https://github.com/UCR-CS122A/lab2/blob/main/lab2.png)

## Submission
You do not need to clone this repo. Go to the "lab-common" submodule and press the "Use  this template" at the top right. This will allow you to make a new private repo with any name you want. When it is time to submit, push your code to your repo and then you can submit on gradescope, using your github repo.
