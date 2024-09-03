Computers can do 2 things:
- store state
- manipulate state -> done with **[[Arithmetic Logic Unit (ALU)]]**

### Binary Addition Circuit for one bit slice
Usually when we want to add 2 n-bit binary numbers we start from the least-significant bits of each number
- '2' cannot be represented with 1 bit, so carry most significant bit from addition to next position
- need 2 output bits to represent sum of bits
	- sum bit
	- carry bit
#### Half Adder:
Represented by the following truth table:
c - carry bit
s - sum bit

| x   | y   | c   | s   |
| --- | --- | --- | --- |
| 0   | 0   | 0   | 0   |
| 0   | 1   | 0   | 1   |
| 1   | 0   | 0   | 1   |
| 1   | 1   | 1   | 0   |
Performs only half the job of addition, hence called half adder
#### [[Full Adder (FA)]]

To continue addition operation to next position, 3 bits must be added together: x, y, cin
This operation can output binary numbers 0-3
Circuit represented by the following truth table is called a Full Adder

| x   | y   | cin | cout | s   |
| --- | --- | --- | ---- | --- |
| 0   | 0   | 0   | 0    | 0   |
| 0   | 0   | 1   | 0    | 1   |
| 0   | 1   | 0   | 0    | 1   |
| 0   | 1   | 1   | 1    | 0   |
| 1   | 0   | 0   | 0    | 1   |
| 1   | 0   | 1   | 1    | 0   |
| 1   | 1   | 0   | 1    | 0   |
| 1   | 1   | 1   | 1    | 1   |
Implemented using logic gates

### N-bit binary addition circuits
 To perform N-bit binary addition, we chain N full adders together
 i.e. 4 bit addition uses 4 full adders and 8 bit addition uses 8 full adders

### [[Multiplexer (MUX)]]
Common pattern in hardware design to compute multiple values in parallel and choose value you need using a multiplexer (MUX)
Collection of values we want to select from are called **data inputs**
MUX that receives N data inputs will need $log_2N$ **selection input** bits to encode which data input to select
Data inputs are labeled with decimal number subscripts w/ zero indexing
Selection inputs labeled with subscripts that correspond to exponents of N-bit unsigned binary positional notation

### Buses and N-but wide MUXes
To represent N-bit signals, wires are bundled into groups called **buses**
- buses represented as a wire with a slash through it labeled w/ the # of wires in the bus

### 1-bit [[Logic Unit]]
logic unit: module that lets us choose between L bitwise logical operations
- implemented by creating a 1-bit logic unit then replicating same module many times for N-bit logic unit
- ex: 32-bit logic unit needed to perform bitwise logical operations on 32-bit int variables
1-bit logic unit implemented by performing each of the bitwise logical operations we wish to perform and select the one we actually want to use with a multiplexer
- sounds counterintuitive, but actually fastest way to perform computations in hardware
implementation:

| s   | o       |
| --- | ------- |
| 00  | a AND b |
| 01  | a OR b  |
| 10  | a NOR b |
| 11  | a XOR b |
### [[Arithmetic Logic Unit (ALU)]]
Performs all of the arithmetic operations and bitwise logical operations taught so far
Data - **what** information we are processing
Control - **which** operation to perform in processing data
ALU takes in 2 pieces of data (A & B) and produces one new piece of data. 
- use control bits to decide which operation to perform
To build:
1. design 1-bit arithmetic unit  and 1 bit logic unit
2. chain those circuits together
### ALU (cont.)
ALU combines [[Full Adder (FA)]] , XOR gates, [[Multiplexer (MUX)]], and [[Logic Unit]] to create a circuit that lets us choose between a set of basic arithmetic operations and bitwise logical operations
**Sub** is a control signal
- makes circuit perform addition when 0 and subtraction when 1
	- when `Sub==0` XOR gates do not complement $B_i$ signals so adders perform `A+B`
	- when `Sub==1` XOR gates do complement $B_i$ signals, so adders perform `A+~B` 
- is an input to the least significant $c_{in}$ which adds 1 when `Sub==1`
When `Sub==1` the adders perform `A+~B+1 = A+(~B+1) = A-B` 
### N-bit ALU
N-bit ALUs are made by chaining together N 1-bit ALUs
- each 1-bit ALU receives different bits from the buses, but every 1-bit ALU receives the same **control** signal 
### Example and explanation
![[1bitALU 1.png]]Bottom table shows how to use Logic unit
**Full Adder:** A = 0, B = 1 XOR 0 = 1, Cin = 1 (carry bit), so Sum = 0 and Cout (remainder) = 1
**Logic Unit:** A = 0, B = 1, R = 2, so NOR, A NOR B = ~(A OR B) = 0, output = 0. 

**MUX:** input 1 into mux, so output from MUX is 0
