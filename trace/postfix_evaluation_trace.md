# Trace: Stack-Based Postfix Evaluation

## Overview
This document traces the direct stack-based postfix evaluation algorithm as implemented in the `evaluatePostfix()` function of [`src/expression_tree.c`](../src/expression_tree.c).

The input expression is:
```text
8 3 2 * + 6 2 / -
```

## Algorithm Description
1. Scan the postfix string token by token from left to right.
2. If the scanned character is a space `' '`, skip it.
3. If the character is an operand (digit checked via `isdigit()`):
   - Convert character to integer value (`symbol - '0'`).
   - Push the integer onto the operand stack (`stack[++top]`).
4. If the character is an operator (`+`, `-`, `*`, `/`):
   - Pop the top element into `b` (right operand): `b = stack[top--]`.
   - Pop the next top element into `a` (left operand): `a = stack[top--]`.
   - Compute `result = operation(a, b, symbol)`.
   - Push `result` back onto the stack: `stack[++top] = result`.
5. Upon reaching the null terminator `'\0'`, the final evaluated result is stored at `stack[top]`.

---

## Step-by-Step Trace Table

| Step | Symbol | Operation | Stack after operation |
| :---: | :---: | :--- | :--- |
| 1 | `8` | Push 8 | 8 |
| 2 | `3` | Push 3 | 8, 3 |
| 3 | `2` | Push 2 | 8, 3, 2 |
| 4 | `*` | 3 × 2 = 6 | 8, 6 |
| 5 | `+` | 8 + 6 = 14 | 14 |
| 6 | `6` | Push 6 | 14, 6 |
| 7 | `2` | Push 2 | 14, 6, 2 |
| 8 | `/` | 6 ÷ 2 = 3 | 14, 3 |
| 9 | `-` | 14 - 3 = 11 | 11 |

---

## Detailed Step Walkthrough

1. **Token `8` (Operand):**
   - Push `8` onto stack.
   - Stack: `[8]` (top points to 8).

2. **Token `3` (Operand):**
   - Push `3` onto stack.
   - Stack: `[8, 3]` (top points to 3).

3. **Token `2` (Operand):**
   - Push `2` onto stack.
   - Stack: `[8, 3, 2]` (top points to 2).

4. **Token `*` (Operator):**
   - Pop right operand: `b = 2`.
   - Pop left operand: `a = 3`.
   - Compute: `3 * 2 = 6`.
   - Push `6` onto stack.
   - Stack: `[8, 6]`.

5. **Token `+` (Operator):**
   - Pop right operand: `b = 6`.
   - Pop left operand: `a = 8`.
   - Compute: `8 + 6 = 14`.
   - Push `14` onto stack.
   - Stack: `[14]`.

6. **Token `6` (Operand):**
   - Push `6` onto stack.
   - Stack: `[14, 6]`.

7. **Token `2` (Operand):**
   - Push `2` onto stack.
   - Stack: `[14, 6, 2]`.

8. **Token `/` (Operator):**
   - Pop right operand: `b = 2`.
   - Pop left operand: `a = 6`.
   - Compute: `6 / 2 = 3`.
   - Push `3` onto stack.
   - Stack: `[14, 3]`.

9. **Token `-` (Operator):**
   - Pop right operand: `b = 3`.
   - Pop left operand: `a = 14`.
   - Compute: `14 - 3 = 11`.
   - Push `11` onto stack.
   - Stack: `[11]`.

## Final Result
- End of expression reached.
- Result returned from `stack[top]`: **`11`**.
