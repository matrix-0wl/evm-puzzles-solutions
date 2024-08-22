# Puzzle 3

```js

00      36      CALLDATASIZE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      5B      JUMPDEST
05      00      STOP

? Enter the calldata:
```

This puzzle introduces the `CALLDATASIZE` opcode, which retrieves the size of the calldata (the data sent with the transaction) in bytes and pushes that size onto the stack. Since there's a `JUMPDEST` located at position 4, the calldata needs to be 4 bytes long to reach it. Any 4-byte calldata will work, such as `0xFFaaFFaa`.
