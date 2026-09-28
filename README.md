# Expression Tree Construction and Evaluation

A comprehensive implementation and comparative study of **Expression Tree Construction and Evaluation** versus **Direct Stack-Based Postfix Evaluation** in C for Data Structures and Algorithms.

---

## Objective
To implement an Expression Tree from a given postfix expression, perform tree traversals (Inorder, Preorder, Postorder), evaluate the expression using both Stack-based evaluation and Expression Tree evaluation, and compare both techniques based on operations, complexity, and structural preservation.

---

## Problem Statement
Given the postfix arithmetic expression:
```text
8 3 2 * + 6 2 / -
```
1. Construct a Binary Expression Tree using an explicit pointer stack.
2. Display tree traversals:
   - Inorder Traversal
   - Preorder Traversal
   - Postorder Traversal
3. Evaluate the expression using:
   - Direct Stack-based Postfix Evaluation
   - Bottom-up Expression Tree Evaluation
4. Generate comprehensive trace tables capturing intermediate steps.
5. Provide rigorous asymptotic complexity analysis and comparative evaluation.

---

## Postfix Expression
```text
8 3 2 * + 6 2 / -
```

---

## Technologies Used
- **Language:** C (C99 / C11 standard)
- **Standard Library:** `<stdio.h>`, `<stdlib.h>`, `<ctype.h>`, `<string.h>`
- **Compiler:** GCC (MSYS2 / MinGW / Linux GCC / Clang)

---

## Expression Tree Diagram

```text
          -
         / \
        +   /
       / \ / \
      8  * 6  2
         / \
        3   2
```

---

## Traversals

- **Inorder Traversal:**
  ```text
  8 + 3 * 2 - 6 / 2
  ```
- **Preorder Traversal:**
  ```text
  - + 8 * 3 2 / 6 2
  ```
- **Postorder Traversal:**
  ```text
  8 3 2 * + 6 2 / -
  ```

---

## Evaluation Results

- **Stack-based Postfix Evaluation:** `11`
- **Expression Tree Evaluation:** `11`

---

## Trace Tables
Detailed step-by-step intermediate traces are documented in the `trace/` directory:
- [Stack-Based Postfix Evaluation Trace](trace/postfix_evaluation_trace.md)
- [Expression Tree Construction Trace](trace/expression_tree_construction_trace.md)
- [Expression Tree Evaluation Trace](trace/expression_tree_evaluation_trace.md)

---

## Complexity Analysis
- [Complexity Analysis Document](analysis/complexity_analysis.md)
  - Time Complexity: $\mathcal{O}(n)$ for both direct stack evaluation and tree-based evaluation.
  - Space Complexity: $\mathcal{O}(n)$ space for tree storage and stacks; $\mathcal{O}(h)$ recursive auxiliary space during tree evaluation.

---

## Comparison
- [Comparison Table](analysis/comparison_table.md)
  - Detailed side-by-side metric comparison covering data structures, operations count (5 operands, 4 operators, 9 tokens), memory models, and structural features.

---

## Conclusion
- [Final Conclusion](docs/final_conclusion.md)
  - Both approaches accurately yield the result **11**. Direct stack-based postfix evaluation computes the result with minimal overhead in a single pass, but destroys syntactic relationships. In contrast, the Expression Tree maintains the complete hierarchical syntax structure, enabling multiple traversals, symbol manipulations, and expression reusability.

---

## Repository Structure

```text
expression-tree-postfix-evaluation/
│
├── README.md
│
├── src/
│   └── expression_tree.c
│
├── input/
│   └── input.txt
│
├── output/
│   └── output.txt
│
├── trace/
│   ├── postfix_evaluation_trace.md
│   ├── expression_tree_construction_trace.md
│   └── expression_tree_evaluation_trace.md
│
├── analysis/
│   ├── complexity_analysis.md
│   └── comparison_table.md
│
└── docs/
    └── final_conclusion.md
```

---

## How to Compile and Run

### Compilation
Using GCC:
```bash
gcc src/expression_tree.c -o expression_tree
```

### Execution
- **On Windows:**
  ```cmd
  expression_tree.exe
  ```
- **On Linux / macOS:**
  ```bash
  ./expression_tree
  ```

### Expected Output
```text
Postfix Expression: 8 3 2 * + 6 2 / -

Inorder Traversal: 8 + 3 * 2 - 6 / 2 
Preorder Traversal: - + 8 * 3 2 / 6 2 
Postorder Traversal: 8 3 2 * + 6 2 / - 

Stack-based Postfix Evaluation: 11
Expression Tree Evaluation: 11
```
