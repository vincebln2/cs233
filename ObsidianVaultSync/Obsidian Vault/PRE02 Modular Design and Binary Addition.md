* The same bit string can mean many different things
	* ex: N-bit unsigned binary can only represent positive integers and n-bit  2's complement can represent both positive and negative integers
Cannot perform true addition or subtraction with either representation, we perform modular arithmetic
- can result in errors called overflow when using very large numbers
- we use modular design to make large circuits

**Truth table to Boolean expressions**
Use sum of products method
* variable - - a letter or expression in bool expression that represents 0 or 1
* Product term - an AND of 1 or more var or complemented var
* Sum-of-Products - an OR of 1 or more product terms
* 
To perform:
- find every row in truth table with output of 1
- create product term
- or all product terms together

| A   | B   | f(A, B) | Product |
| --- | --- | ------- | ------- |
| 0   | 0   | 0       |         |
| 0   | 1   | 1       | A'B     |
| 1   | 0   | 0       |         |
| 1   | 1   | 1       | AB      |
f(A,  B) = A'B + AB

**Positional Notation**
-  Value of symbols in this notation is determined by position relative to the radix point (aka decimal point in decimal)

**Binary Representation**
Binary is a base 2 positional notation using only 0 and 1 (each symbol in a binary number is called a bit)

**Hexadecimal Representation**
Base 16 positional notation that uses symbols 0-9 and A-F 
- useful because 16 = 2^4, meaning four bits equals one hexdecimal digit
Indicated by prefacing hexadecimal numbers with 0x to indicate base

**Converting between hexadecimal and decimal**
- use positional notation interpretations to do the conversion
example:
$$
0x514 = 5*16^2 +1*16^1+4*16^0 = 1300
$$
**Converting between hexadecimal and binary**
Cluster binary bits into groups of 4 starting from the least significant bit (add extra leading zeros if needed)
example:
100101010 => 0001 0010 1010 => 0x12A

**Decimal to Binary Conversion**
- perform mod2 on current decimal number and record the result
- divide decimal number by 2, round down, get new current decimal number
- if current decimal number != 0, repeat starting performing mod2 until
- collect remainders from end to beginning to construct binary representation of the number
similar process to go from decimal to hexadecimal, except you use mod16'

**Two's complement representation**
- most significant bit has a negative weight, negative numbers have a 1 in the most significant bit position, otherwise all positive num have 0

**Overflow**
def: any time desired math result does not match reality of what our circuits give us
circuits perform modular arithmetic, if circuits dont match expected result this is called mismatch overflow

**N-Bit unsigned binary arithmetic**
very similar to decimal addition, carry 

**Zero extension and sign extension**
languages like c use different bit widths for different variable types, type casting can increase or extend the bit width of a num
zero extension - adding zeros to front of most significant bits without changing the value of a number

Sign extension - adding copies of the sign bit in front of most significant bits without changing value

**N-bit unisgned and Nbit two's complement representations in c/c++**
*reminder, two's complement number system uses most significant bit as sign*
unsigned char - 8 bit unsigned binary
char - 8bit two complement
unsigned short - 16 bit unisigned binary 
short - 16 bit two complement
unsigned int - 32 bit unsigned binary
int - 32 bit two's complement
unsigned long - 61 bit unsigned binary
long - 64 bit two's complement representation

**Bit-Shifting**
used to manipulate data at bit level or for performing arithmetic operation like multiplying or dividing by powers of 2

Left Shift
interpreted as multiplying number by 2^1

Right Shift
interpreted as dividing number by 2^1

**Modular design**
typically work with 32 bit or 64 but var and numbers