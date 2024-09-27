## Implementing the combinational blocks for my custom CPU.

This week I've started to port the Hack computer from the nand2tetris course to Verilog. My goal was to only use the built-in nand gate and build every other block from there.

In this first week I've built all the fundamental gates (and, or, nor, xor, not...) some multiplexers (mux, mux16, dmux...), some combinational circuits (half adder, full adder, add16, inc16) and finally the ALU. I've also tested every one of them except the ALU that I have to test still.
I've developed them using a plain text editor, iverilog for compiling it and gtkwave to visualize the result. 

![add16 snippet in Verilog.](/media/add16_snippet.png)

There are some gates were I can test all the possible inputs but there are others (like add16 or the ALU) where it's impractical. In those cases I've used randomised inputs.

![XOR gate test bench waves.](/media/xor_testbench_snippet.png)
![ALU test benchwaves.](/media/alu_testbench_snippets.png)

These first steps feel very basic but as I wanted every bit of the computer from the nand gate I've spent a lot of time implementing a lot of repetitive blocks as it can be the case with Or8Way, Mux16, Dmux16, etc. 

The next step for the next week would be to fully test the ALU and start implementing the memory part of the computer.
You can check the progress at: [my github repo](https://github.com/marc-marcos/von-neumann-cpu-verilog) 