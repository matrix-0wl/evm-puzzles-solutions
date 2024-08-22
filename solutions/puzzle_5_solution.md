# Puzzle 5

```js

00      34          CALLVALUE
01      80          DUP1
02      02          MUL
03      610100      PUSH2 0100
06      14          EQ
07      600C        PUSH1 0C
09      57          JUMPI
0A      FD          REVERT
0B      FD          REVERT
0C      5B          JUMPDEST
0D      00          STOP
0E      FD          REVERT
0F      FD          REVERT

? Enter the value to send: (0)
```

Here we have a `JUMPI`, which is a conditional jump. The `JUMPI` instruction will conditionally modify the program counter based on the value of the second element on the stack. If this element is `1`, the jump occurs; if it’s `0`, it doesn’t. The first stack element determines the jump destination. During this process, `JUMPI` consumes both of these values from the stack. In our puzzle, the `PUSH1 0x0C` above provides the correct destination address, so we just need to ensure the condition value is `1`. Looking at the previous lines:

- `CALLVALUE` pushes a value onto the stack
- `DUP1` duplicates it, so the stack now has two identical values
- `MUL` multiplies these two values, effectively squaring the call value
- `PUSH2 0x0100` pushes `0x0100` (which is 256 in decimal) onto the stack
- `EQ` compares the top two stack items, which are 256 and the square of our call value

Thus, setting a `CALLVALUE` of 16 results is a successful outcome.
