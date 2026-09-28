# Final Conclusion

## Summary of Results
Both the **Stack-Based Postfix Evaluation** and the **Expression Tree Evaluation** implemented in [`src/expression_tree.c`](../src/expression_tree.c) successfully evaluated the postfix expression:
```text
8 3 2 * + 6 2 / -
```
Both techniques yielded the identical, mathematically correct result: **`11`**.

---

## Technical Insights and Synthesis

1. **Direct Stack-Based Postfix Evaluation:**
   - Evaluates the postfix stream sequentially in a single pass.
   - Operates with minimal overhead by reducing intermediate subexpressions immediately into scalar values on an integer stack.
   - Highly memory-efficient and fast for single-shot arithmetic evaluation, but it is destructive: intermediate syntactic relationships, operator precedence, and operand groupings are discarded as computation progresses.

2. **Expression Tree Evaluation:**
   - Constructs a persistent, hierarchical binary tree representation in memory before evaluation.
   - Internal nodes represent operators, and leaf nodes represent operands.
   - Preserves explicit operator precedence and associativity without needing parentheses.
   - Retains the full syntax structure, allowing:
     - **Multiple Traversals:** Inorder traversal produces infix form (`8 + 3 * 2 - 6 / 2`), preorder traversal produces prefix form (`- + 8 * 3 2 / 6 2`), and postorder traversal regenerates postfix form (`8 3 2 * + 6 2 / -`).
     - **Reusability:** The tree can be evaluated repeatedly with varying variable bindings, transformed, or symbolically simplified (e.g., constant folding, dead code elimination, compiler abstract syntax tree passes).

3. **Suitability:**
   - **Direct Stack Evaluation** is best suited for resource-constrained environments, calculators, virtual machine execution engines (e.g., JVM bytecode execution), and simple one-time postfix interpreters.
   - **Expression Trees** are the foundational data structure for compilers, mathematical expression parsers, computer algebra systems (CAS), and optimization frameworks where structural manipulation, tree rewriting, and multi-format traversals are required.
