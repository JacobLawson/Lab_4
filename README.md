Lab_4
=====
##### Design
------------------------------------------------------------------------
###Discussion of ALU Modifications

The ALU design was pretty straightforward. I went off the recommendation of the Lab Handout to do a case statement.
I then created a different case for each input of OpSel that would go into the ALU and I then created different outcomes
depending on what the input was. Another notable example is that the LDI and LDAI instructions became LD. This is because we did not have anything to load into the data register, so we just combined the instructions together

###ALU Test and Debug

After doing the above, I ran the simulation. I ran into some syntax errors initially with the ror operation as I did
not make the Accumulator value unsigned, I just did Accumulator ror. After I fixed that everything went as planned and the 
waveform results matched the original, or expected, values from the lab handout as can be seen below.

![alt text] (http://i59.tinypic.com/2uy3xfp.png)


I verified the results by going through each line and checking the instructions. For example, when OpSel=110, the operation
is a LD, which is supposed to load the value from data into the accumulator. The waveform does this for when data is equal
to 1010 and 1011, which indicates the operation was successful.

###Discussion of Datapath Modifications

For the Datapath modifications, there were no significant ones like there were for the ALU. The design of the Datapath went on based on the given example for the PC and the given diagram in the handout. The IR register for example had IRLd as the input sign for changing the values in the register to the data. When IRLd and Clock and Clock 'event all equaled one, the output became data as could be seen in the diagram. This example was followed to create the rest of the registers and outputs.

###Datapath Test and Debug

The test for the datapath ran well for every value except for the Addr line. This line kept having UU hex as the assigned value up until about 100ns. The problem was that the case statement did not concatenate the MARHi and MARLo values when AddrSel was equal to one. Instead it tried to set bits 7 to 4 to MARhi and 3 to 0 to MARLo. Eventually I consulted Taylor Bodin, who said that one could try concatenating the two signals instead of assigning them to separate bits. I then used the & operand to concatenate the two signals and that produced the correct waveform in the end.

###Discussion of Testbench Operation

After correcting the above, I ran the simulation again to run the testbench. I had to comment out a few extra semicolons in the testbench code in order to make it correct with regards to syntax. Afterwards I ran the code and got the results below

![alt text] (http://i61.tinypic.com/sg2wli.png)

As with the ALU test bench, I went through each instruction set and I made sure that the registers and the outputs had the expected values before deciding to continue further with the lab. After comparing results with what was expected with what was on the waveform, I did an overall visual confirmation to ensure the 0 to 50ns timeframe matched the waveform provided in the lab handout.

##### Reverse Engineering

###Program listing from 0 to 700ns

From 0 to 25 ns, nothing is going on as the IR is 00 and there is NOP

From 26 to 55ns, the LDAI function is going on as the IR reads 7, which is IR in the PRISM manual.
This can be evident from the hex value B being loaded into the Accumulator by the time this IR is over.

From 56 to 85ns, the IR reads 3, which indicates ROR. This can be evident from looking at the diagram which has the accumulator have a value of 1011 and then change to 1101, or from b to d in hex values

From 86 to 125 ns, the IR reads 4, which indicates OUT. The data eventually loads the value of the accumulator into
itself, which then disappears, presumably to the output port.---

From 126 to 145ns, the IR reads 0, which means there are no operations going on.

From 146 to 195ns, the IR reads d, which means that STA is going on. This is apparent through the accumulator staying at d, which is then loaded onto the IR. STA is then followed by b because b was loaded into the data register afterwards

From 196 to 240 ns, the IR reads b, which indicates a JN. This is apparent through the 2 value being recognized as negative by Alesszero, which then prompts the IR to jump to Addr 2, which RORs the 2 into a 3 for the next set of instructions

The above steps repeat over and over again until the accumulator reads a value of 7, which occurs around 625ns.

From 625 ns onwards, the IR reads 9 which indicates a JMP. The jump will go to c since that is the last instruction passed along.



then detailed instructions for 0 to 50 ns, and the jump later at 225ns
