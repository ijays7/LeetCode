## Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.



**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## Solution

题目是让设计一个栈满足常规的 push、pop、top 以及获取栈中最小的元素。

这道题最简单的方法是内部存储两个栈，其中一个栈负责常规的 push、pop 和 top 操作，另外一个栈负责维护最小的元素，仅仅在栈为空或者比当前栈顶元素更小时入栈。

其中入栈、出栈和获取栈顶元素的时间复杂度都是 O(1) 的。

```java
public class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minStack;


    /**
     * initialize your data structure here.
     */
    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();

    }

    public void push(int x) {
        stack.push(x);

        if (minStack.isEmpty() || minStack.peek() <= x) {
            minStack.push(x);
        }

    }

    public void pop() {
        if (stack.isEmpty()) {
            return;
        }
        if (stack.peek().equals(minStack.peek())) {
            // 栈顶元素
            minStack.pop();
        }
        stack.pop();
    }

    public int top() {
        if (stack.isEmpty()) {
            return 0;
        }
        return stack.peek();
    }

    public int getMin() {
        if (minStack.isEmpty()) {
            return 0;
        }

        return minStack.peek();

    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

