## Sequential blocks, cheating, cheating and visualization.

This week (or a couple of weeks), I've continued to advance on the Von Neumann Verilog computer, building some of the sequential circuits that will be needed to implement it. Specifically, I've implemented: a bit, a 16-bit register, an 8 words RAM, a 64 words RAM, a 512 words RAM, a 4096 (4k) words RAM and a 16384 words RAM.

One of the premises of this project was to build the computer entirely from NAND gates, and by building the first sequential block, I've already broken that premise, the first cheating. 

The DFF is a circuit that follows a simple behavior: out(t+1) = in(t). This may seem simple, but it changes everything I've done so far. The outputs of the circuit are now not only determined by the current state of the circuit, but also by earlier inputs.

In the nand2tetris course, this bit was a given, and as that was the case, at the start of the week I also used it as a given. Basically, the output of the bit instead of being always the input of the last clock cycle, it's the input of the last clock cycle where load equalled 1. Instead of implementing it with the structural modeling I was supposed to use (gate-level) I searched a bit and used behavioral modeling and data flow modeling. These forms of modeling are much higher-level than gate-level, so although I've used them here, I don't plan to use them unless necessary. 

![bit snippet in Verilog.](/media/bit_snippet.png)

The next block to build is the register. Which is basically a group of 16 bits, it behaves like a bit but is 16 bits wide. 

![Register testbench waveform in GTK Wave.](/media/register_testbench.png)

The next five blocks are basically implemented the same, but with exponential growth. To implement the RAM8 we just have 8 registers and first a Dmux to conduct the load signal only to the register that the address bits select and then a Mux to conduct all the outputs from all the registers and select only the one we selected with address.

![RAM8 snippet in Verilog.](/media/RAM8_snippet.png)

The other RAM chips are implemented exactly the same but changing the registers to bigger RAM chips. For example, to implement the RAM64 instead of using 8 registers, I used 8, RAM8 chips (8x8 = 64), and to implement the RAM4K I used 8 RAM512 (8x512 = 4096). 

These designs fetch 8 memory addresses at the same time, if we were doing serious CPU design, taking in account delays and such, here we could improve our RAM design by using those other 7 addresses we don't want if the following access is to one of those, for example. 

One problem that arose with the larger designs (4k and 16k) is that they are uncompilable. That's the second cheating I'm going to do this week. With the RAM4K we use 780447 NAND gates (71955 NOT gates, 124894 AND gates, 65520 OR gates and 262144 NAND gates) and my computer can't really compile it. To solve this issue I've decided to resort, again, to behavioral modeling. I've understood how the RAM4K is built with logic gates, but in the implementation I will use the implementation of the next image to be able to compile it.

![RAM4K snippet in behavioural Verilog.](/media/RAM4K_snippet.png)

To build the RAM16K module, instead of using the gate-level RAM4K, I've used the behavioral RAM4K, making the compile process instantaneous. I don't really count this one as cheating because I've built it also with gates, but I don't have the patience to wait 45 minutes for it to compile.

Another thing that I might look into when I finish the project is changing the mux's and demux's from inside the RAM from 8way into 16way, and seeing what performance impact that has. Smaller RAM chips needed to the same capacity. I might also make some parts of the computer, if not the whole computer, in Logisim, to be able to visually look at the circuits, rather than having to look at them through the wave forms.

The next step in the project will be designing and implementing the machine language for the CPU.
