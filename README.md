Lab_4
=====
##### Design
------------------------------------------------------------------------
###Discussion of ALU Modifications

The ALU design was pretty straightforward. I went off the recommendation of the Lab Handout to do a case statement.
I then created a different case for each input of OpSel that would go into the ALU and I then created different outcomes
depending on what the input was. 

###ALU Test and Debug

After doing the above, I ran the simulation. I ran into some syntax errors initially with the ror operation as I did
not make the Accumulator value unsigned, I just did Accumulator ror. After I fixed that everything went as planned and the 
waveform results matched the original, or expected, values from the lab handout as can be seen below.

![alt text] (http://i59.tinypic.com/2uy3xfp.png)


I verified the results by going through each line and checking the instructions. For example, when OpSel=110, the operation
is a LD, which is supposed to load the value from data into the accumulator. The waveform does this for when data is equal 
to 1010 and 1011, which indicates the operation was successful.

###Discussion of Datapath Modifications

###Datapath Test and Debug

###Discussion of Testbench Operation
