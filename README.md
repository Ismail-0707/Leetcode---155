# LeetCode 155 - Min Stack

## Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

All operations must run in **O(1)** time complexity.

---

## Example

### Input
```text
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
```

### Output
```text
[null,null,null,null,-3,null,0,-2]
```

---

## Approach

We use **two stacks**:

1. **Main Stack**
   - Stores all elements.

2. **Min Stack**
   - Stores the minimum element at each stage.

### Logic
- While pushing:
  - Push element into main stack.
  - If min stack is empty or current value is smaller/equal, push into min stack.
- While popping:
  - If popped value equals min stack top, remove from min stack too.
- `getMin()`:
  - Return top of min stack.

---

## Java Solution

```java
import java.util.*;

class MinStack {

    Stack<Integer> stack;
    Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int val) {

        stack.push(val);

        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {

        if (stack.peek().equals(minStack.peek())) {
            minStack.pop();
        }

        stack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

---

## Complexity Analysis

- **push()** → `O(1)`
- **pop()** → `O(1)`
- **top()** → `O(1)`
- **getMin()** → `O(1)`

### Space Complexity
- `O(n)`

---

## Key Concept

The second stack (`minStack`) always keeps track of the minimum element till the current position, allowing `getMin()` to work in constant time.
