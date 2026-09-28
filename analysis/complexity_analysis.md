# Complexity Analysis

This document provides a formal asymptotic time and space complexity analysis of both approaches implemented in [`src/expression_tree.c`](../src/expression_tree.c):
1. Direct Stack-based Postfix Evaluation (`evaluatePostfix`)
2. Expression Tree Construction (`constructTree`) and Evaluation (`evaluateTree`)

Let $n$ denote the total number of tokens (operands and operators) in the postfix expression, and $h$ denote the height of the constructed binary expression tree. For an expression of $n$ tokens, $n = 9$ (5 operands and 4 operators), and the tree height $h = 3$ (where height of single node is 0 or edges from root to deepest leaf).

---

## 1. Stack-Based Postfix Evaluation

### Time Complexity: $\mathcal{O}(n)$
- The algorithm processes the postfix string in a single linear pass of length proportional to the string size ($n$ tokens).
- For each token:
  - Checking if it is an operand (`isdigit`) takes $\mathcal{O}(1)$ time.
  - Pushing an operand onto the stack takes $\mathcal{O}(1)$ time.
  - Popping two operands, evaluating a basic arithmetic operation (`+`, `-`, `*`, `/`), and pushing the result back takes $\mathcal{O}(1)$ time.
- Total Time Complexity: $\mathcal{O}(n)$.

### Space Complexity: $\mathcal{O}(n)$
- The algorithm utilizes an integer stack array `stack[MAX]`.
- In the worst case (e.g., all operands appear before operators), the stack stores up to $(n + 1) / 2$ operands simultaneously.
- Auxiliary Space Complexity: $\mathcal{O}(n)$.

---

## 2. Expression Tree Approach

The Expression Tree approach operates in two distinct phases:

### Phase 1: Expression Tree Construction (`constructTree`)

#### Time Complexity: $\mathcal{O}(n)$
- The postfix string is scanned token-by-token from left to right.
- For each operand token:
  - Node allocation (`createNode`) via `malloc` takes $\mathcal{O}(1)$ time.
  - Pushing the node pointer onto `treeStack` takes $\mathcal{O}(1)$ time.
- For each operator token:
  - Node allocation takes $\mathcal{O}(1)$ time.
  - Popping two pointers (`right` and `left`) takes $\mathcal{O}(1)$ time.
  - Assigning `left` and `right` child pointers takes $\mathcal{O}(1)$ time.
  - Pushing the new root pointer onto `treeStack` takes $\mathcal{O}(1)$ time.
- Across $n$ tokens, exactly $n$ nodes are created and connected in linear time: $\mathcal{O}(n)$.

#### Space Complexity: $\mathcal{O}(n)$
- **Tree Storage:** Exactly $n$ `struct Node` structures are dynamically allocated on the heap, requiring $\mathcal{O}(n)$ memory.
- **Stack Storage:** The auxiliary pointer stack `treeStack[MAX]` stores up to $\mathcal{O}(n)$ node pointers during construction.
- Overall Space Complexity for Construction: $\mathcal{O}(n)$.

---

### Phase 2: Expression Tree Evaluation (`evaluateTree`)

#### Time Complexity: $\mathcal{O}(n)$
- The function `evaluateTree` performs a postorder traversal over the expression tree.
- Each of the $n$ nodes in the tree is visited exactly once.
- At each node, a constant number of operations are performed (checking base case or executing `operation(leftValue, rightValue, root->data)`).
- Total Evaluation Time Complexity: $\mathcal{O}(n)$.

#### Space Complexity: $\mathcal{O}(h)$ Auxiliary Stack Space
- Because `evaluateTree` is implemented recursively, the runtime call stack grows proportional to the height of the tree $h$.
- In the best/balanced case, $h = \mathcal{O}(\log n)$.
- In the worst-case (skewed expression tree), $h = \mathcal{O}(n)$.
- Recursive Auxiliary Space: $\mathcal{O}(h)$.
- Overall space including the existing tree structure on heap: $\mathcal{O}(n)$.

---

## 3. Comparative Summary of Asymptotic Complexities

| Method | Phase | Time Complexity | Auxiliary Space Complexity | Total Space Complexity |
| :--- | :--- | :---: | :---: | :---: |
| **Stack-Based Postfix Evaluation** | Direct Evaluation | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ |
| **Expression Tree Approach** | Construction | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ |
| | Evaluation | $\mathcal{O}(n)$ | $\mathcal{O}(h)$ | $\mathcal{O}(n)$ |
| | **Total Combined** | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ |

---

## 4. Key Asymptotic and Practical Observations

1. **Identical Asymptotic Class:**
   Both approaches belong to the same asymptotic complexity classes: $\mathcal{O}(n)$ time and $\mathcal{O}(n)$ space.
2. **No Claim of Superior Asymptotic Efficiency:**
   The Expression Tree approach does **not** have better asymptotic complexity than direct postfix evaluation.
3. **Constant Factor Overhead:**
   The direct stack evaluation performs a single pass with minimal integer stack operations and zero dynamic memory allocations. In contrast, the expression tree approach requires two full passes (construction pass + recursive evaluation pass), dynamic memory allocations (`malloc`), and pointer chasing, resulting in higher constant factors in runtime and memory consumption.
4. **Structural Advantage:**
   While computationally heavier for a one-off evaluation, the Expression Tree's explicit $\mathcal{O}(n)$ heap representation persists the hierarchical precedence structure, enabling tree traversals (inorder, preorder, postorder), algebraic simplifications, expression transformations, and repeated evaluations with different variable bindings without re-parsing.
