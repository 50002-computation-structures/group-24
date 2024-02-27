[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/5YTzVbxp)
## 50.002 1D Project Group (group 24)

|Student Id | Name|
|-----------|-----|
|1006887 | Manimoliyan Elankumuthan|
|1007195 | Chan Wei Ping|
|1007189 | Augustine Lim King Hwee|
|1006965 | Tan Yi Xuan, Xavier|
|1006621 | Ng Yu Hueng|
|1007144 | Priyanshi Saraogi|
|1007114 | Jithin Bathula|


16 bit ALU

Building a 16 bit Arithimetic Logic Unit using Lucid.

### General outline of ALU
1. Adder/Subtractor Unit
2. Compare Unit
3. Boolean Unit
4. Shifter Unit
5. Multiplier Unit
6. Modulus Unit (Extra)

# Input of ALU: 
1. 16 bit binary number A
2. 16 bit binary number B
3. 6 bit binary number alufn

ALUFN OPCODE:
| Operation |	ALUFN[5:0] |
|-----------|------------|
|ADD|000000|
|SUB|000001|
|AND|011000|
|OR|011110|
|XOR|010110|
|“A”|011010|
|SHL|100000|
|SHR|100001|
|SRA|100011|
|CMPEQ|110011|
|CMPLT|110101|
|CMPLE |110111|
|MUL|100010|

# Output of ALU:
1. 1 bit boolean Z
2. 1 bit boolean V
3. 1 bit boolean N
4. 16 bit binary out

# Steps to operate ALU
1. Io-dip[0][0] = 1 and press the middle button for manual mode or just press the middle button for auto-test.
![photo_2024-02-27 11 18 58](https://github.com/50002-computation-structures/group-24/assets/132822321/5e73bdba-4e70-40a6-9875-55a0041811a3)


2. While in auto-test mode, if io-dip[2][7] = 1: it creates a false test case and the auto test will fail
![photo_2024-02-27 11 19 01](https://github.com/50002-computation-structures/group-24/assets/132822321/7e413a75-0658-4903-8c8b-d8e921bb0f23)


3. When in manual mode, input 16-bit binary value in io-dip[0:1] for A when A is shown on the 7-segment display and then press the middle button.
![photo_2024-02-27 11 18 57](https://github.com/50002-computation-structures/group-24/assets/132822321/6b9b2d52-150d-419e-9a4a-1daba98f07c0)


4. Input 16-bit binary value in io-dip[0:1] for B when b is shown on the 7-segment display and then press the middle button.
![photo_2024-02-27 11 18 59](https://github.com/50002-computation-structures/group-24/assets/132822321/cb93f809-a351-4ad7-bc76-ad69164274dd)


5. Input 6-bit binary value in io-dip[0] for alufn when OP is shown on the 7-segment display and then press the middle button. 
![photo_2024-02-27 11 19 00](https://github.com/50002-computation-structures/group-24/assets/132822321/5e0a4645-a356-42ca-afd0-eb2cd619a68e)


6. 7-segment[0:2] will show the z, v, n respectively. The led[0:1] will output the 16 bit binary output. led[2] will display the alufn.


### Other Details

# Adder/Subtractor Unit:
```
Either adds a to b or subtracts a from b depending on alufn[0]

Input: a, b, alufn[0]
Output: sum, z, v, n
  
sum is a 16 bit binary number
*sum might overflow
  
if (alufn[0] == 0):
    sum = a+b
if (alufn[0] == 1):
    sum = a-b
    
z is true if all bits of sum are 0
v is true if there is an overflow during calculation
n is true if sum is a negative number
```

# Compare Unit:
```
Checks if a is equal to, less than, less than or equal to b depending on alufn[2:1]

Input: a, b, alufn[2:1]
Output: cmp
  
cmp is a 1 bit boolean value

Comparison   alufn[2:1]
  A = B        110011
  A < B        110101
  A <= B       110111

if (output of comparison is true):
    cmp[0] = 1
if (output of comparison is false):
    cmp[0] = 0
```

# Boolean Unit:
```
Outputs boolean operations such as AND, OR, XOR, "A", on a and b

Input: a, b, alufn[5:0]
Output: bool

bool is a 16 bit binary number

bool applies the logic based on alufn[5:0]

Operation   alufn[5:0]
  AND         11000
  OR          11110
  XOR         10110
  “A”         11010
```

# Shifter Unit
```
Outputs a after it has been shifted by b bits. The type of shift depends on alufn[1:0]

Input: a, b, alufn[1:0]
Outut: shift
  
shift is a 16 bit binary number which is a after it has been shifter by b bits
  
Operation                               alufn[1:0]
SHL (shift left)                            00
SHR (shift right)                           01
SRA (shift right with sign extension)       11
```

# Multiplier Unit
```
Performs a multiplication between 16-bit input a and b and outputs a 16-bit value.

input: a, b, alufn[1:0]
output: mul

mul is a 16-bit binary number
*overflow will occur and only the 16 lowest significant bit will be taken

mul = a * b
```

# Modulus Unit
```
Modulus is not part of the basic ALU and has been added as an additional feature. Outputs Modulus of a and b where they are both 16 bits inputs.

Input: a, b, alufn[2:0]
Output: out

out is a 16 bit binary number
```
