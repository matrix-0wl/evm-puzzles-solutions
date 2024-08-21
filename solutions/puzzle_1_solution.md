# Puzzle 1

```js

00      34      CALLVALUE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      80      JUMPDEST
05      80      DUP1
06      00      STOP

? Enter the value to send: (0)

```

To explain the process, let's break it down:

1. **CALLVALUE Instruction**: The `CALLVALUE` opcode retrieves the value of the current call (i.e., the amount of ether sent with the transaction) in wei and places this value on top of the stack. For example, if the transaction is sent with 5 wei, then the value `5` will be pushed onto the stack.

2. **JUMP Instruction**: The `JUMP` opcode takes the top value from the stack and uses it to determine the position in the code to jump to. This position is represented by a program counter. The `JUMP` instruction must target a valid `JUMPDEST` (jump destination) opcode; otherwise, the contract will revert. The program counter will jump to the location indicated by the value at the top of the stack.

3. **Solving the Puzzle**: To solve the problem, we need to invoke the contract with `msg.value` set to 8 wei. Here's why:

   - When the contract is called with `msg.value = 8`, the `CALLVALUE` instruction pushes the value `8` onto the EVM stack.
   - The `JUMP` instruction then pops this `8` from the stack and uses it as the target position for the program counter.
   - The program counter jumps to the instruction at position 8, which must be a `JUMPDEST` instruction, ensuring that the program execution continues safely from that point.

By setting `msg.value` to 8, we correctly set up the conditions needed for the `JUMP` instruction to move to the correct instruction (`JUMPDEST`), allowing the contract to proceed without errors.
