# Background
## Introduction to Verilog & SystemVerilog

### Key Primitives

Verilog and SystemVerilog (SV) both expose primitive types that can be synthesized into registers, wires, discrete gates, adders, etc. Most of these primitives overlap with C-like syntax. However, we introduce two primitives that are unique and very important to these HDLs (hardware desciprion languages).

| Verilog | SV | Purpose |
|---|---|---|
| `wire` | `wire` | Primitive which physically connects components together. **Cannot** be _assigned_ a value. Can be driven by multiple signals at once. |
| `reg` | `logic` | Primitive that can be _assigned_ a value. Cannot be driven by multiple signals at once. |

A common point of confusion in Verilog is that `reg` always synthesizes to a register. This is **not** true. You must dissocate the concepts of `reg` and register.

In Verilog (and SV) `reg` represents a primitive that can be _assigned_ a value. Whether this primitive synthesizes to a register depends on how it's used within the `always` block.

SystemVerilog was introduced to offer both greater functionality, and greater clarity of the primitives from  Verilog. For this reason, SV added a new type: `logic` that serves as a replacement for `reg`.

### Modules 
Throughout this class, you will have labs where you will need to write your own Verilog modules. [Here](https://nandland.com/introduction-to-verilog-for-beginners-with-code-examples/) is a quick and basic tutorial from Nandland that goes over how to make a module in Verilog.

In the tutorial above, the module is defined with all the input/ouput signals but they aren't declared as inputs or ouputs until the next lines. You can actually do these two steps together resulting in the following definition:
```verilog
module example_and_gate  
(   
  input input_1,  
  input input_2,  
  output and_result
);
```
Looking at the above, you will notice that the inputs and outputs are not actually given a type. In most situations, the default type for Verilog is `wire` however in SystemVerilog this is `logic`(more on SystemVerilog later). Even if you plan on using the default type, we recommend that you initialize the variable type as well, making it easier to figure out what kind of varible it is when reading through the code.

```verilog
module example_and_gate  
(   
  input wire input_1,  
  input wire input_2,  
  output wire and_result
);
```

### Always Blocks
Always blocks are commonly used in verilog. [Here](https://nandland.com/always-blocks-for-beginners/) is another quick tutorial from Nandland about always blocks for combinational logic.

The tutorial above mentions something called a "Sensitivity List". Something that you might want to use is the `*` operator in the sensitivity list(example: `always @(*)`). This actually sets all the signals that are read from, into the sensitiity list so you don't have to list each one.

At the end of the tutorial, there is a link to a tutorial for Always Blocks for Sequential Code. Although we will be using combinational logic for this lab, we recommend you go over this to better understand the difference between combinational and sequential logic.

There are multiple Always blocks, each one are used for a different purpose. And SV has updated the names from Verilog to be more descriptive in terms of how the blocks are updated.

| Verilog | SV | Purpose |
|---|---|---|
| `always` | `always` | Syntax for declaring a logic block that executes at every tick. Used only in simulation. Cannot be synthesized. |
| `always @(*)` | `always_comb` | Syntax for declaring combinational logic block. Assignments in this block synthesize to wires |
| `always @(posedge <signal>)` | `always_ff @(posedge <signal>)` | Syntax for declaring sequential logic block. Assignments within this block synthesize to registers (flip flops). |

### Case Blocks
Case statements are similar to switch statements in C. [Here](https://nandland.com/case-statement-2/) is an example of a case statement being used in Verilog.

## Testbenches
Testbenches are used to test your code before you synthesize it. These testbenches are just verilog files that are used to drive the simulation. They usually create an instance of the module you created and run some test inputs through it.

You will have to make your own testbench for lab 2, using the template provided. For this lab, you will not need the `clk` variable since we did not use sequential logic. Any line that use the `clk` variable can be removed for this lab. At the top of the file, after the testbench module is declared, you can initialize any variable you will need. After that, you need to create an instance of the module that you are testing and connect some signals to its inputs and outputs. The sample testbench does not give the top module a name. You will need to do so. 

After creating an instance of your top module, you will need to set the `CLK_PERIOD`. This will be used to control the time between each of your tests. Once those are set, you can add your tests in the `initial` block. The line with `#(CLK_PERIOD*3);` essentially sets a delay for 3 times the CLK_PERIOD. To add a test, you should set your input signals to a specific value. You can then add a delay as seen before so that the result remains for a bit before moving on to the next test. You will be able to see the results in the simulation when you run `make top.sim`.

>Note: you can see a sample testbench in the blinky sample directory used in lab 1

## System Verilog
The Nandland tutorials go over Verilog, however, we will be using SystemVerilog for this class. SystemVerliog builds ontop of Verilog, so anything from the Nandland tutorials should still work in SystemVerilog. We will be using SystemVerilog because it adds some features that are nice to use, such as the `logic` data type which can replace `wire` and `reg` types in many situations. `logic` variables can be assigned with either continuous  assignemnts(the `assign` opperation used in the first Nandland tutorial above) or in procedural blocks(using the `<=` or `=` operators shown in the Always Block and Case Statement tutorials).
