# 4-Bit-ALU
Custom 4-Bit ALU


## Making the required gates

This is a 4 bit ALU i made from scratch designed as a prototype/proof of concept for a final 8 bit ALU i will integrate into an upcoming custom cpu project

### OR gate
First, i needed to make an OR gate as i started with exclusively AND and NOT gates (2 fundemental gates):
Using De Morgan's theorem it was very easy to implement by using NOT((NOT A) AND (NOT B)) to create an OR gate.

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/f8ffe4c4-9d9d-4cc3-88a7-463389015c55)

### XOR gate
An XOR gate was also fairly simple to make,
it requires an or gate, with 2 AND gates coming from it, AND-A being (A AND NOT B), AND-B being (NOT A AND B).

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/41cdb29e-1f9d-4d39-84f2-3e250dc38ea2)

That is all the gates we need

## making the adder
first of all we need to make a 4-Bit Adder, which is comprised of 4 Full-Adders which are in turn comprised of 2 Half adders each.

### Half adder
A half adder is simply a normal adder without a Carry input.
The SUM output of the half adder is the result of (A XOR B) and the CARRY output is the result of (A AND B)
this makes a binary 1 with 1 input and a binary 2 with 2 inputs

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/2886f65c-94d9-4a9b-8ba9-da970fed51cb)

### Full adder
A full adder is slightly more complex, it is made up of 2 half adders and 3 inputs. IN-A and IN-B both go into the Half-Adder-A.
Then SUM-A goes into IN A for Half-Adder-B as well as Carry-IN goes into B for Half-Adder-B.
Carry-OUT is the result of (Carry-A OR Carry-B).
SUM is the result of SUM-B

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/79e7765c-5a60-4da2-933f-ae96e30c820c)

### 4-bit adder
For ease of understanding we will be using the FUll adder chip from now on to make our circuitry Neater and more readable.
We will be compiling the 4 Bit adder into a module as well so we can more easily deal with added complexity.

the 4 bit adder is very simple, it works by having 4 full adders, corresponding to Adder-A being for A0 and B0 inputs, Adder-B corresponding to A1 and B1 as inputs,
with SUM-A being S, SUM-B being S1 ect..
C-IN goes into Carry-In-A then chains through Adders B,C,D then ending at C-OUT.

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/dc00d8ee-f36f-4a52-ae70-d367ea806d1d)

## Final ALU
Now for the final composition of the 4-Bit ALU chip.

### Features of the ALU
our ALU has 4 bit addition as well as 4 bit subtraction with negative number theory and 3 conditionals.
our conditionals are 3 outputs that light up if our number is 0 or if our number is negative, as well as a carry.

### building the ALU 
building it is simple, 
simply add the 8 total inputs (Nibble-A and Nibble-B) and input 9 (a subtract button).
Place a 4 bit adder first then the following.
connect the first nibble straight to the 4 bit adder.
connect Nibble-B to 4 XOR gates leading to the adder and the subtract button to the other side of each. 
Meaning the input is unchanged with 0 on the subtract input (SUB from now on).
However, when the SUB button is pressed, it is also wired to the Carry-In of the 4 bit adder, 
this means it bitwise XORs the second nibble and adds 1, effectively converting it into two's compliment negative.
That is our add and subtract functions done,
We then chain 3 and gates together to make a 4-way AND gate and take our 4 output bits and branch them, NOT the new branches of our output nibble and feed it into the 4 way and gate to check for a 0 output. The Negative test is connected to the most significant bit as we are using two's compliment.
our carry condition is then wired directly up to the 4 bit adder carry out.

![image](https://github.com/gbentham06/4-Bit-ALU/assets/169713724/1616eb5e-9324-428b-9531-2f67ac4f30a9)


