# Puzzle 2

```js

00      34      CALLVALUE
01      38      CODESIZE
02      03      SUB
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      5B      JUMPDEST
07      00      STOP
08      FD      REVERT
09      FD      REVERT

? Enter the value to send: (0)

```

There's a new instruction to consider: `CODESIZE`. This opcode pushes the size of the contract's code onto the stack. In this case, the size of the code is 10 bytes (even though the last line is labeled 09, it starts from 00).

The `SUB` instruction takes the two values at the top of the stack and subtracts the second one from the first. In this scenario, the operation being performed is `CODESIZE - CALLVALUE`.

We see that there's a `JUMPDEST` at position 06. To jump to this point, the calculation must satisfy the equation: `CODESIZE - CALLVALUE = 10 - CALLVALUE = 6`.

Thus, the correct `CALLVALUE` needed for this operation is 4 Wei.
