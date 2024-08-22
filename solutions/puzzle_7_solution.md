# Puzzle 7

```js
00      36        CALLDATASIZE
01      6000      PUSH1 00
03      80        DUP1
04      37        CALLDATACOPY
05      36        CALLDATASIZE
06      6000      PUSH1 00
08      6000      PUSH1 00
0A      F0        CREATE
0B      3B        EXTCODESIZE
0C      6001      PUSH1 01
0E      14        EQ
0F      6013      PUSH1 13
11      57        JUMPI
12      FD        REVERT
13      5B        JUMPDEST
14      00        STOP

? Enter the calldata:
```

The first 4 lines copy the entire calldata into memory. The following 4 lines create a contract using the initialization code that was just loaded into memory from the calldata. Essentially, the first 10 lines are responsible for creating a contract based on the provided calldata.

Next, the subsequent 3 lines verify whether the `EXTCODESIZE` is exactly 1 byte. The contract being checked is the one just created with the `CREATE` instruction, which also pushes the new contract's address onto the stack. It's important to note that `EXTCODESIZE` measures the size of the contract's runtime code, not its initialization code. The challenge is to ensure that this size is 1 byte. To achieve this, we need to construct `CALLDATA` for a contract that results in a runtime code of exactly 1 byte. The key is to design the constructor to produce runtime code that is precisely 1 byte in length.

In EVM assembly:

- `0x60 01` (PUSH1 0x01) - Push the length `0x01` onto the stack.
- `0x60 00` (PUSH1 0x00) - Push the offset `0x00` onto the stack.
- `0xF3` (RETURN) - Return the byte from the stack.

So, the full constructor bytecode is:

```
0x60 01 60 00 F3
```

So, the input we need to give is `0x60016000F3`.
