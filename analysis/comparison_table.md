# Comparative Analysis

This document provides a comparative analysis of **Stack-Based Postfix Evaluation** and **Expression Tree Evaluation** for the postfix expression:
```text
8 3 2 * + 6 2 / -
```

---

## Metric Breakdown for the Expression
- **Number of Operands:** 5 (`8`, `3`, `2`, `6`, `2`)
- **Number of Operators:** 4 (`*`, `+`, `/`, `-`)
- **Total Tokens / Nodes:** 9
- **Evaluated Result:** 11

---

## Detailed Comparison Table

| Metric / Parameter | Approach A: Stack-Based Postfix Evaluation | Approach B: Expression Tree Evaluation |
| :--- | :--- | :--- |
| **Method** | Direct single-pass stack evaluation (`evaluatePostfix`) | Two-stage tree construction (`constructTree`) and recursive evaluation (`evaluateTree`) |
| **Data Structure Used** | Array-based integer stack (`int stack[MAX]`) | Binary Tree (`struct Node` nodes with `left` and `right` pointers) and pointer stack (`treeStack[MAX]`) |
| **Number of Operands** | 5 | 5 |
| **Number of Operators** | 4 | 4 |
| **Main Operations** | Array index pushes, pops, and inline arithmetic calls (`operation()`) | Dynamic allocation (`malloc`), pointer manipulation, child linking, recursive function calls |
| **Time Complexity** | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ (Construction $\mathcal{O}(n)$ + Evaluation $\mathcal{O}(n)$) |
| **Space Complexity** | $\mathcal{O}(n)$ (Integer stack array) | $\mathcal{O}(n)$ (Heap node allocations) + $\mathcal{O}(h)$ (Recursive call stack) |
| **Structural Information** | **None:** Discarded immediately as intermediate values are reduced to scalars | **Preserved:** Full syntax hierarchy, operator precedence, associativity, and parent-child dependencies |
| **Traversal Support** | **None:** Postfix stream is consumed linearly and once | **Full:** Inorder (infix), Preorder (prefix), and Postorder (postfix) traversals supported |
| **Result** | **11** | **11** |

---

## Discussion of Differences

1. **Memory & Runtime Overhead:**
   - Stack-based evaluation operates directly with fixed memory and contiguous integer storage. It has low cache misses and zero dynamic allocation overhead.
   - The Expression Tree allocates separate heap blocks for each token, uses pointers, and relies on recursive call frames, incurring higher constant-factor execution and memory overhead.

2. **Utility and Reusability:**
   - If the task is strictly a one-time numerical evaluation of a postfix expression, direct stack evaluation is optimal and simpler.
   - If the expression must be inspected, printed in infix/prefix notation, symbolically differentiated, optimized, or repeatedly evaluated with varying variable bindings, the Expression Tree provides the necessary structural representation.
