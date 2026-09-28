# Trace: Expression Tree Evaluation

## Overview
This document traces the recursive evaluation of the constructed Expression Tree as implemented in the `evaluateTree()` function of [`src/expression_tree.c`](../src/expression_tree.c).

## Evaluation Mechanism
The function `evaluateTree(struct Node *root)` performs a bottom-up (postorder) evaluation of the tree:
1. **Base Case / Operand:**
   - If `isdigit(root->data)`, return numeric value: `root->data - '0'`.
2. **Recursive Traversal:**
   - Evaluate left child: `leftValue = evaluateTree(root->left)`.
   - Evaluate right child: `rightValue = evaluateTree(root->right)`.
3. **Operator Computation:**
   - Compute `operation(leftValue, rightValue, root->data)` and return the result to the caller.

---

## Evaluation Trace Table

| Step | Subexpression | Operation | Result |
| :---: | :--- | :--- | :---: |
| 1 | `3 * 2` | 3 × 2 | 6 |
| 2 | `8 + 6` | 8 + 6 | 14 |
| 3 | `6 / 2` | 6 ÷ 2 | 3 |
| 4 | `14 - 3` | 14 - 3 | 11 |

---

## Detailed Call Stack and Order of Evaluation

The recursive postorder traversal unfolds as follows:

1. **Visit Root (`-`):**
   - Must evaluate left subtree (`+`) and right subtree (`/`).

2. **Evaluate Left Subtree of Root (`+`):**
   - Left child is leaf `8` $\rightarrow$ returns `8`.
   - Right child is subtree `*`:
     - Left child of `*` is leaf `3` $\rightarrow$ returns `3`.
     - Right child of `*` is leaf `2` $\rightarrow$ returns `2`.
     - Computes `3 * 2 = 6` $\rightarrow$ returns `6`.
   - Computes `8 + 6 = 14` $\rightarrow$ returns `14`.

3. **Evaluate Right Subtree of Root (`/`):**
   - Left child of `/` is leaf `6` $\rightarrow$ returns `6`.
   - Right child of `/` is leaf `2` $\rightarrow$ returns `2`.
   - Computes `6 / 2 = 3` $\rightarrow$ returns `3`.

4. **Compute Root Operation (`-`):**
   - `leftValue = 14`
   - `rightValue = 3`
   - `14 - 3 = 11`.

## Final Result
- The function returns **`11`**.
