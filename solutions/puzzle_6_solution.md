# Puzzle 6

```js

00      6000      PUSH1 00
02      35        CALLDATALOAD
03      56        JUMP
04      FD        REVERT
05      FD        REVERT
06      FD        REVERT
07      FD        REVERT
08      FD        REVERT
09      FD        REVERT
0A      5B        JUMPDEST
0B      00        STOP

? Enter the calldata:
```

`CALLDATALOAD` loads a 32-byte value from the specified byte offset. If the 32-byte value extends beyond the length of the calldata, the extra bytes are automatically set to `0`.

The offset to be loaded is determined by the value at the top of the stack, provided here by the `PUSH1 0x00` instruction above. Essentially, the calldata itself should contain the destination address for the `JUMP`. Our `JUMPDEST` is located at `0x0A`, so that should be our calldata.

However, remember that any overflowing bytes are set to `0`. If we simply send `0x0A`, the remaining 31 bytes will become `00`, resulting in `0x0A00000000000000000000000000000000000000000000000000000000000000`, which is a very large number!

Instead, we should left-pad with zeros and send `0x000000000000000000000000000000000000000000000000000000000000000A` as our calldata. This way, reading 32 bytes from the zero offset will correctly yield `0x0A`.
