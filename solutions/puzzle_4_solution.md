# Puzzle 4

```js

00      34      CALLVALUE
01      38      CODESIZE
02      18      XOR
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      FD      REVERT
07      FD      REVERT
08      FD      REVERT
09      FD      REVERT
0A      5B      JUMPDEST
0B      00      STOP

? Enter the value to send: (0)

```

We know that `CALLVALUE` will push the value we enter onto the top of the stack. We can also determine the `CODESIZE` by looking at the number of instructions. In this program, there are 12 instructions, which equals 12 bytes or `0x0C` in hexadecimal, and this value is pushed to the stack. The `JUMPDEST` is located at 10 (`0x0A` in hexadecimal). Now, let's examine the `XOR` instruction. `XOR` compares two numbers in their binary form and returns a 1 in each bit position where the bits of either, but not both, operands are 1. That's why we need to find a `CALLVALUE` that, when XOR'ed with `0x0C`, gives `0x0A`.

Converting `0x0C` to binary gives `00001100`.
Converting `0x0A` to binary gives `00001010`.

Bit by bit, XOR'ing `00001100` with `00001010` results in `00000110`, which is `0x06` in hexadecimal. Therefore, we need a `CALLVALUE` of 6.
