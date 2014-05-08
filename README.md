ECE281_CE5
==========


| Assembly        | Bits           | Machine Code  |
| ------------- |:-------------:| -----:|
| addi $s0, $0, 44  | 001000 00000 10000 0000000000101100   | 0x2010002C |
| addi $s1, $0, -37 | 001000 00000 10001 1111111111011011   | 0x2011FFDB |
| add $s2, $s1, $s0| 000000 10000 10001 10010 00000 100000 | 0x02119020 |
| sw $s2, 0x54($0)  | 101011 00000 10010 0000000000110110   | 0xAC120054 |

![](https://github.com/C16erikthompson/ECE281_CE5/blob/master/Waveform.png?raw=true)

The first two cycles show the instructions for the 44 and -37 taking place, loading them into registers.  The next cycle shows the result of the addition, 7, being stored into a resgister.  The last relevant cycle shows this value being overwritten by the 54.  (was looking at the wd value)

 
#Task 3

To Complete this task, both the ALU and the datapath must be altered.  To start, the datapath and ALU decoders were altered to recognize the ORI and OR instructions as shown in the table below

![](https://github.com/C16erikthompson/ECE281_CE5/blob/master/ALUinstr.png?raw=true)


My first attempt at implementing the ORI instruction involved adding a bit extender and increasing the size of the ALU.  Unable to get this to perform properly, I found that the ORI can be accomplished by using the or function of the alu and writing the result to a register as you would any immediate type.  Using this method, no modifications had to be made to the schematic.

To implement my design in vhdl, the following lines of code had to be added:

Process (op) begin
 case op is
 
 .....
 
 when "001101" => controls <= "101000011"; -- ORI
 
 .....
 
 case aluop is
 
 ....
 
 when "10" => alucontrol <= "001"; -- or (for ori) 
 
 ....
 
 
To test my design I inserted the following instructions into the test bench

     	  instr <= X"2010002C"; -- adding 44 to $s0
        wait for clk_period;
        
        instr <= X"3612FFDB"; -- ORI $s0 with -37
        wait for clk_period;
        
This code produced the following waveform when simulated:

![](https://github.com/C16erikthompson/ECE281_CE5/blob/master/Waveform2.png?raw=true)

By the value in spot 18 in memory is the result of the ori instruction.  It is shown to be a success, with a '1' for every bit in the result.
