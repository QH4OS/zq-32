# Registers
```
| Name     | Use                                                      |
| r0       | Reads as zero, write are ignored                         |
| r1 - r11 | General purpose                                          |
| rf       | Flags register                                           |
| ri       | Stores the address of the next instruction               |
| rv       | Stores the interrupt vector (if zero interrupts disabled |
| rt       | Stores the return vector for interrupts |
```
## Flags Register Layout
```
znco0000000000000000000000000000

z = zero flag
n = negative flag
c = carry flag
o = overflow flag
```
# Instruction Encoding
```
RRR Instructions
cccooooxxxxyyyy1zzzz000000000000

RRI Instructions
cccooooxxxxyyyy0iiiiiiiiiiiiiiii

c = condition field
o = opcode
x = register
y = register
z = register
i = 16 bit signed imm that can act as z
```
## Condition Field
```
Only runs the instruction if the flags match the field
| Encoding | ZF | NF | CF | OF |
| 000      | ?  | ?  | ?  | ?  |
| 001      | ?  | 0  | ?  | ?  |
| 010      | 0  | ?  | ?  | ?  |
| 011      | 0  | 0  | ?  | ?  |
| 100      | 0  | 1  | ?  | ?  |
| 101      | 1  | 0  | ?  | ?  |
| 110      | ?  | ?  | 1  | ?  |
| 111      | ?  | ?  | ?  | 1  |
```
## Operations Field
```
0000 Add: A = B + C (Changes zero, carry, overflow, negative flag)
0001 Sub: A = B - C (Changes zero, carry, overflow, negative flag)
0010 And: A = B & C (Changes zero and negative flag)
0011 Or: A = B | C (Changes zero and negative flag)
0100 Xor: A = B ^ C (Changes zero and negative flag)
0101 Lod: A = [B + C]
0110 Str: [B + C] = A 
0111 shl: A = B << C (Shifts into carry flag before falling)
1000 shr: A = B >> C (Shifts into carry flag before falling)
1001 rol: A = B rol C 
1010 ror: A = B ror C
```
# IO
## Interrupts
```
On a interrupt these occur:
1: rt = ri
2: ri = rv
3: rv = 0 (to disable further interrupts)
```
## Devices
### Keyboard
```
- When a keypress happens the single interrupt on the cpu fires
- At address 0xFFFFFFFF
- A read will give each keypress in a FIFO configuration, and return 0x00 if no keypress is in buffer
```
### Frame Buffter
```
- Each pixel in the 320x200
```
### Text Out
