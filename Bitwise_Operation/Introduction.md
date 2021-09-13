# Introduction

In computer programming, a bitwise operation operates on a bit string, a bit array or a binary numeral at the level of its individual bits. It is a fast and simple action basic to the higher level arithmetic operations and directly supported by the processor. Most bitwise operations are presented as two-operand instructions where the result replaces one of the input operands.

On simple low-cost processors, typically, bitwise operations are substantially faster than division, several times faster than multiplication, and sometimes significantly faster than addition. While modern processors usually perform addition and multiplication just as fast as bitwise operations due to their longer instructions pipelines and other architectural design choices, bitwise operations do commonly use less power because of the reduced use of resources.

## Convert  between Decimal and binary 

E.g. (166)~10~ to binary

Divide by the base 2 to get the digits from the remainders:

| Division by 2 | Quotient | Remainder(Digit) | Bit # |
| ------------- | -------- | ---------------- | ----- |
| (166)/2       | 83       | 0                | 0     |
| (83)/2        | 41       | 1                | 1     |
| (41)/2        | 20       | 1                | 2     |
| (20)/2        | 10       | 0                | 3     |
| (10)/2        | 5        | 0                | 4     |
| (5)/2         | 2        | 1                | 5     |
| (2)/2         | 1        | 0                | 6     |
| (1)/2         | 0        | 1                | 7     |



= (10100110)~2~  (write the reminder backward)

convert back

1 * 2^7^ + 0 * 2^6^  + 1 * 2^5^ + 0 * 2^4^ + 0 * 2^3^ + 1 * 2^2^  + 1 * 2^1^ + 0 * 2^0^ = 128 + 32 + 4 + 2 = 166

## Bitwise Operator

| Action             | Operator | Example                                       |
| ------------------ | -------- | --------------------------------------------- |
| OR                 | \|       | (00101)<br /> OR (10110)<br /> =     (10111)  |
| AND                | &        | (00101)<br />And (10110)<br />=      (00100)  |
| NOT                | ~        | NOT (10110)<br />=       (01001)              |
| Exclusive OR (XOR) | ^        | (00101)<br />XOR (10110)<br />=       (10011) |
| left shift         | <<       | <<     (00101)<br /> =      (01010)           |
| right shift        | >>       | >>     (00101)<br /> =      (00010)           |

### Exclusive OR (XOR)

A bitwise XOR is a binary operation that takes two bit patterns of equal length and performs the logical exclusive OR operations on each pair of corresponding bits. The result in each position is 1 if only one of the bits is 1, but will be 0 if both are 0 or both are 1. In this we perform the comparison of two bits, being 1 if the two bits are different, and 0 if they are the same. In cryptography, one of the operand in XOR operation can be viewed as an instruction of the other. if 1, its instruction is to flip the bit at that position. Otherwise, it keeps the original bit at that position.

x ^ 0 = x (nothing is flipped)

x^(~0) = ~x (every bit is flipped)

x^(~x) = (~0) (all the bits are 1s. ~x would flip every 0 to 1 and keep original 1s)

x^x = 0 (every 1 are flipped)

If c = a ^ b, a ^ c = b and b ^ c = a

a\^b\^c = a\^(b\^c) = (a\^b)\^c

Application of bitwise operation

| Action                                                       | Equations                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Set last n bits of x to be 0 (count from most significant bit) | x & (~0 << n)                                                |
| get the nth bit of x                                         | (x >> n) & 1                                                 |
| keep the nth bit and set others to 0                         | x & (1 << (n -1) )                                           |
| set the nth bit to 1                                         | x \| (1 << n)                                                |
| set the nth bit to 0                                         | x & (~(1 << n))                                              |
| only keep bits after the nth bit and set others to 0 (nth bit is excluded) | x & ((1 << n) - 1)                                           |
| set all bits after the nth bit to 0  (nth bit is included)   | x & (~ ((1 << (n + 1))- 1))                                  |
| Determine odd or even                                        | Odd: (x & 1) == 1 or x % 2 == 1<br />Even: (x & 1) == 0 or x % 2 == 0 |
| Divide by 2                                                  | x/2 == x >> 1                                                |
| flip the first bit from right (lowest) that equals to 1      | x & (x - 1)                                                  |
| get the first bit from right that equals to 1                | x & (-x)   (-x = ~x + 1, the lowest bit would be kept)       |
| remove all bits                                              | x^x<br />x & (~x)                                            |
| Find the smallest power of 2 that is greater than or equal to n | check below                                                  |

 ```java
     private int toNearst2power(int n) {
         // the following is for integer only
         // for long you might go up to 32
         n--;
         n |= n >> 1;
         n |= n >> 2;
         n |= n >> 4;
         n |= n >> 8;
         n |= n >> 16;
         return n + 1;
     }
 ```

