# Traversing-Linked-List-and-Binary-Tree-using-Digital-Circuit
## Digital Circuit for Linked List
### Problem Statement
- The basic problem statement is traversing a linked list and finding the maximum value smaller than an input number X.  
- The linked list is fed in the form of a binary file through a ROM starting from address 0, where address A holds the node value and address A+1 stores the address of the next node.  
- The entire circuit has to be made using the 7400 IC series which includes IC's like Multiplexers, Registers, Counters, Flip Flops, combinational gates etc. ([Entire Problem Statement](https://github.com/san2130/Digisim21/blob/main/Digisim'21_PS1.pdf))

### Approach
The circuit was designed on **Proteus** EDA software.

- On a high level, the basic approach is to iterate over the entire linked list and check if the current node value is smaller than the input X and then update the maximum such value.  
- The linked list will be read through the ROM which takes an address as input and returns the data stored at that address.  
- Since the hardware cost for the ROM is high only one ROM was used to read both the node value and the address of the next node.  
- Thus there will be two types of data as the ROM output, the node value which will be then proccessed using combinational logic and the address of the next node which will be fed back to the ROM and the cycle goes on until the ROM output is 255(end of list)  

The data of the ROM can be changed by using this [python file](https://github.com/san2130/Digisim21/blob/main/create_bin_file.py). 
Running this script will generate [PS1.bin](https://github.com/san2130/Digisim21/blob/main/PS1.bin) which can be loaded into the ROM.  
<br>

**TRAVERSING THROUGH LINKED LIST**  
- An adder was used to increase the current address by 1 and then give that address to the
ROM with the help of a MUX. 
- The MUX has two input lines - current address and current address + 1, and a select line which is the current mode. 
- Mode 0 maps to the ROM output being the current node value while Mode 1 corresponds to the ROM output being the address of the next node.  
- This mode toggles on every cycle, therefore the time taken to move to the next node is 2 clock cycles.
<br>

**CALCULATION**  
<br>
Now, we just have to calculate the maximum bank amount which Harshad Mehta can repay.
- When the mode is 0 it means the ROM output is a node value so this value is then sent to the combinational logic. 
- The node value is compared with the current holdings of Harshad (X) using a comparator, if this value is less than or equal to X then it is further compared with the maximum such node value encountered so far stored in a register and accordingly this register is updated. 
 

Now, we have our required result in binary form, we just have to show it on 7 segment display. Before that we have to convert it into BCD.
For 7 segment display we will use **Shift Add 3 method**. You can read about it [here](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/Binary2BCD.pdf).
<br>

### Solution  
You can find complete proteus file [here](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/ps1.DSN).
<br>
### Working  
You can see the working video of our circuit [here](https://drive.google.com/file/d/1smdCNSce_toEbJcSIwCuEU5kZWQFbrIi/view?usp=sharing).
We have used the data give in [problem statement](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/Digisim'21_PS1.pdf).


## Digital circuit for Binary Tree-
### Problem Statement-
We have to implement a **Binary Tree** data structure using the digital circuit components like mux, gates, registers e.t.c.
Please, read the complete problem statement [here](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/Digisim'21_PS2.pdf) to understand what exactly we have to do.
### Approach-
We will simulate our circuit on EDA tool **Proteus**.

We have a ROM which act as a memory device for this circuit. Its store all the values of linked list corresponding to there addresses. You can change the data of Rom by using [this](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/python%20image%20file.py) python file. It will create [binary_file_PS2_t1.bin](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/binary_file_PS2_t1.bin) and you have to just load this file on our ROM.

The input of our ROM is connected to the output of an 8-bit 4:1 MUX. The select
line of MUX is a counter of 2-bit (count from 00 to 11). The input of this mux are
the Present node address, Present node address + 1, Present node address +
2.

We also created a 8-bit 8:1 mix whose input are connected to the output of 8 D-
FF connected in series and which store the left and right child node address of
the current node. And the output of this mux is connected to the input of 8-bit 4:1
mux.

So, what is happening? When our clock start, the counter will we at the 00 and it
will give the data of the present node, which is stored in separate D-FlipFlop
after some processing. When our counter increases and go to 10, ROM will give
address of left node which is store in one of the 8 FF connected to 8-bit 8:1 mux
and similarly when counter reaches to 10 the right child node address got
stored.

So, in this way we store all the address of our nodes and process them one by
one by sending them to 8-bit 4:1 mux.
We add one more 8-bit 8:1 mux which will store the value of tpc*distance of
each node.

The data which come out of ROM every time when our counter is at 00 is the
price of petrol and we just have to add the value of tpc*distance into it, which we
do by simple adder and then we compare this value (using comparator) with the
previous data if this is smaller the previous one, we will replace it otherwise do
nothing and whenever we replace data we also store it address in a register
which will become our final address after all nodes are processed.

Now, we have our required result, we just have to show it on 7 segment display.
For 7 segment display we will use **Shift Add 3 method**. You can read about it [here](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/Binary2BCD.pdf).
### Solution-
You can find complete proteus file [here](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/ps2.DSN).
### Working-
You can see the working video of our circuit [here](https://drive.google.com/file/d/1-Hjrgi0n4gRep6W1q02odHNMzv3j3KjB/view?usp=sharing).
We have used the data give in [problem statement](https://github.com/ujjawalece/Implementation-of-Linked-List-and-Binary-Tree-using-Digital-Circuit/blob/main/Digisim'21_PS2.pdf).
