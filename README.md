# V-CPU
**Virtual CPU**

A simple custom virtual CPU with a 16-bit instruction format, assembly syntax, and binary encoding.

---

## Instruction Set & Binary Encoding:

Each instruction is 16 bits:

```text
[ OPCODE (4 bits) ][ R1 (2 bits) ][ R2 (2 bits) ][ IMM / ADDR (8 bits) ]

Register Encoding-
| Register | Binary |
| -------- | ------ |
| R0       | 00     |
| R1       | 01     |
| R2       | 10     |
| R3       | 11     |

Example Program (Assembly → Binary)-
| Assembly           | Binary             |
| ------------------ | ------------------ |
| `LDI R0, 5`        | `0001000000000101` |
| `LDI R1, 1`        | `0001010000000001` |
| `loop: SUB R0, R1` | `0011000100000000` |
| `OUT R0`           | `0111000000000000` |
| `JZ done`          | `0110000000000110` |
| `JMP loop`         | `0101000000000010` |
| `done: HLT`        | `1111000000000000` |

Instruction Reference (ASM → Binary Examples)-
| Instruction | Example      | Binary             |
| ----------- | ------------ | ------------------ |
| `NOP`       | `NOP`        | `0000000000000000` |
| `LDI`       | `LDI R0, 10` | `0001000000001010` |
| `LDI`       | `LDI R1, 10` | `0001010000001010` |
| `LDI`       | `LDI R2, 10` | `0001100000001010` |
| `LDI`       | `LDI R3, 10` | `0001110000001010` |
| `ADD`       | `ADD R0, R1` | `0010000100000000` |
| `ADD`       | `ADD R2, R3` | `0010101100000000` |
| `SUB`       | `SUB R0, R1` | `0011000100000000` |
| `SUB`       | `SUB R3, R2` | `0011111000000000` |
| `MOV`       | `MOV R0, R1` | `0100000100000000` |
| `MOV`       | `MOV R2, R3` | `0100101100000000` |
| `JMP`       | `JMP 5`      | `0101000000000101` |
| `JZ`        | `JZ 8`       | `0110000000001000` |
| `OUT`       | `OUT R0`     | `0111000000000000` |
| `OUT`       | `OUT R1`     | `0111010000000000` |
| `OUT`       | `OUT R2`     | `0111100000000000` |
| `OUT`       | `OUT R3`     | `0111110000000000` |
| `HLT`       | `HLT`        | `1111000000000000` |

Opcode Table-
| Instruction | Opcode |
| ----------- | ------ |
| `NOP`       | `0000` |
| `LDI`       | `0001` |
| `ADD`       | `0010` |
| `SUB`       | `0011` |
| `MOV`       | `0100` |
| `JMP`       | `0101` |
| `JZ`        | `0110` |
| `OUT`       | `0111` |
| `HLT`       | `1111` |

Complete Example:
Assembly-
; Example program
LDI R0, 5
LDI R1, 1

loop:
SUB R0, R1
OUT R0
JZ done
JMP loop

done:
HLT

Raw Binary-
0001000000000101
0001010000000001
0011000100000000
0111000000000000
0110000000000110
0101000000000010
1111000000000000

Output-
Binary loaded into CPU.
OUT: 4
OUT: 3
OUT: 2
OUT: 1
OUT: 0
Program halted.

Notes:
All instructions are 16 bits long.
Labels like loop: and done: are resolved by the assembler.
LDI loads an immediate value into a register.
JMP jumps to a label or address.
JZ jumps when the zero flag is set.
OUT prints the value in a register.
HLT stops execution.
