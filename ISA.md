# Registers
```
| Name     | Use                                        |
| r0       | Reads as zero, write are ignored           |
| r1 - r12 | General purpose                            |
| rf       | Flags register                             |
| ri       | Stores the address of the next instruction |
| rv       | Stores the interrupt vector                |
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
i = 16 bit imm that can act as z
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
