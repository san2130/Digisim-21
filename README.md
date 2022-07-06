# Traversing Linked-List and Binary-Tree using Digital Circuit
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

**Traversing through Linked-List**  
- An adder was used to increase the current address by 1 and then give that address to the
ROM with the help of a MUX. 
- The MUX has two input lines - current address and current address + 1, and a select line which is the current mode. 
- Mode 0 maps to the ROM output being the current node value while Mode 1 corresponds to the ROM output being the address of the next node.  
- This mode toggles on every cycle, therefore the time taken to move to the next node is 2 clock cycles.
<br>

**Calculation**  
<br>
Now, we just have to calculate the maximum bank amount which Harshad Mehta can repay.
- When the mode is 0 it means the ROM output is a node value so this value is then sent to the combinational logic. 
- The node value is compared with the current holdings of Harshad (X) using a comparator, if this value is less than or equal to X then it is further compared with the maximum such node value encountered so far stored in a register and accordingly this register is updated. 
 

Once we have the final answer, we will convert it to 12-bit BCD and display the answer on a seven segment display. 
For 7 segment display we have used **Shift Add 3/Double Dabble Algorithm**. You can read about it [here](/).
<br>

### Solution  
<br>
<p align="center"> <a href=https://github.com/san2130/Digisim21/blob/main/digism21ps1clean.DSN>Proteus Design file</a> <br><br>
<img src="https://github.com/san2130/Digisim21/blob/main/LinkedList.png" width="80%"/></p>
<br>

### Working  
You can see the working video of our circuit [here](https://drive.google.com/file/d/19G4LibBoyWzlmvntwxMMYAmuyDMrrppg/view?usp=sharing).
The binary file used here is [PS1.bin](https://github.com/san2130/Digisim21/blob/main/PS1.bin) and the clock frequency is 5 Hz.


## Digital Circuit for Binary Tree-
### Problem Statement
- The basic problem statement is traversing a binary tree and finding the minimum value of Y = (node_value) + X*(depth of node) where X is an 8-bit input.
- The binary tree is fed in the form of a binary file through a ROM starting from address 0, where address A holds the node value, address A+1 stores the left child while address A+2 stores the right child.
- The entire circuit has to be made using the 7400 IC series which includes IC's like Multiplexers, Registers, Counters, Flip Flops, combinational gates etc. ([Entire Problem Statement](https://github.com/san2130/Digisim21/blob/main/Digisim'21_PS2.pdf))

### Approach
The circuit was designed on **Proteus** EDA software.

- On a high level, the basic approach is to traverse over the entire lbinary tree and check if the value of expense for the current node is lesser than the minimum expense encountered so far and update it accordingly. 
- The binary tree will be read through the ROM which takes an address as input and returns the data stored at that address.  
- Since the hardware cost for the ROM is high only one ROM was used to read both the node value and the address of the children. 
- Thus there will be three types of data as the ROM output, the node value which will be then proccessed using combinational logic and the address of both the children.  
<br>  

**Traversing through Binary-Tree**
- Post-Order Traversal has been implemented using a custom built stack of sixteen 8-bit registers which is the maximum tree size. 
- For every node visited first the right and left children addresses in order, are pushed into the stack if not 255(NULL) and then the current node address is pushed in. 
- If a leaf node is reached then the stack is popped and the address at the top is fed into the ROM, the corresponding node data is then processed using combinational logic. 
- For the depth calculation an additonal stack of sixteen 4-bit registers are used, which pushes in the depth of the current node while going down the tree using a counter. 
- For mulitplying two 8-bit numbers tpc * depth a custom binary mulitplier has been implemented too.
<br>

To display the final answer on a seven segment display the same circuit is used as in the linked-list part to convert 8-bit binary to 12-bit BCD.  
### Solution
<br>
<p align="center"> <a href=https://github.com/san2130/Digisim21/blob/main/Round221clean.DSN</a> <br><br>
<img src="https://github.com/san2130/Digisim21/blob/main/BinaryTree.png" width="80%"/></p>
<br>
### Working
You can see the working video of our circuit [here](https://drive.google.com/file/d/1_hUymDWVhLnb5ABah0CEXrlf9oJ-LaMT/view?usp=sharing).
The binary file used here is [PS2.bin](https://github.com/san2130/Digisim21/blob/main/PS2.bin).
