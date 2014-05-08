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


