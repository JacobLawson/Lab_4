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
