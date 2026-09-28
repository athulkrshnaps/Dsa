# Trace: Expression Tree Construction

## Overview
This document traces the step-by-step construction of the binary expression tree from the postfix expression `8 3 2 * + 6 2 / -`, as implemented in the `constructTree()` function of [`src/expression_tree.c`](../src/expression_tree.c).

## Mechanism of `constructTree()`
The function constructs an expression tree using an explicit stack of node pointers (`treeStack[]`):
1. **Operand Encountered (`isdigit(symbol)`):**
   - A new leaf node is allocated via `createNode(symbol)` with `left = NULL` and `right = NULL`.
   - The node pointer is pushed onto `treeStack`.
2. **Operator Encountered (`+`, `-`, `*`, `/`):**
   - A new operator node is allocated via `createNode(symbol)`.
   - The first popped node becomes the **right child** (`right = pop()`).
   - The second popped node becomes the **left child** (`left = pop()`).
   - The operator node connects its children: `node->left = left` and `node->right = right`.
   - The newly formed subtree root pointer is pushed back onto `treeStack`.
3. **Completion:**
   - When the postfix string finishes, the final tree root is popped from `treeStack` and returned.

---

## Step-by-Step Construction Trace

| Step | Symbol | Operation | Stack/Tree Status |
| :---: | :---: | :--- | :--- |
| 1 | `8` | Create leaf `Node('8')` and push | `[ Node(8) ]` |
| 2 | `3` | Create leaf `Node('3')` and push | `[ Node(8), Node(3) ]` |
| 3 | `2` | Create leaf `Node('2')` and push | `[ Node(8), Node(3), Node(2) ]` |
| 4 | `*` | Pop `right = Node(2)`, Pop `left = Node(3)`. Create `Node('*')`, attach children, and push | `[ Node(8), Subtree(3 * 2) ]` |
| 5 | `+` | Pop `right = Subtree(3 * 2)`, Pop `left = Node(8)`. Create `Node('+')`, attach children, and push | `[ Subtree(8 + (3 * 2)) ]` |
| 6 | `6` | Create leaf `Node('6')` and push | `[ Subtree(8 + (3 * 2)), Node(6) ]` |
| 7 | `2` | Create leaf `Node('2')` and push | `[ Subtree(8 + (3 * 2)), Node(6), Node(2) ]` |
| 8 | `/` | Pop `right = Node(2)`, Pop `left = Node(6)`. Create `Node('/')`, attach children, and push | `[ Subtree(8 + (3 * 2)), Subtree(6 / 2) ]` |
| 9 | `-` | Pop `right = Subtree(6 / 2)`, Pop `left = Subtree(8 + (3 * 2))`. Create `Node('-')`, attach children, and push | `[ Subtree((8 + (3 * 2)) - (6 / 2)) ]` |

---

## Resulting Binary Expression Tree

```text
          -
         / \
        +   /
       / \ / \
      8  * 6  2
         / \
        3   2
```

### Tree Node Structural Properties
- **Total Nodes:** 9
- **Internal Nodes (Operators):** 4 (`-`, `+`, `*`, `/`)
- **Leaf Nodes (Operands):** 5 (`8`, `3`, `2`, `6`, `2`)
- **Root Node:** `-`
- **Left Subtree of Root:** Represents `8 + (3 * 2)`
- **Right Subtree of Root:** Represents `6 / 2`
