## Implement the following operations of a queue using stacks.

Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

## Solution

这道题考的是栈（Stack）和队列（Queue）这两种数据结构。

我们知道栈是先进后出（FILO）的，队列是先进先出（FIFO）的，而这道题是要求用栈这种数据结构去实现一个队列。显然，使用一个栈是无法实现这种需求的，我们至少需要两个栈来实现。

我们使用一个 input 栈来管理入栈，output 栈来管理出栈。当需要进队列的时候我们直接在 input 栈中进行压栈；当需要出队列的时候我们将 input 栈中内容进行出栈，然后在 output 栈中进行入栈，这样进行两次操作后原本应该位于栈底的元素处于了栈顶的位置，相当于负负得正的效果。最后我们将栈顶的元素弹出，即实现了先入先出的效果。peek 的实现同pop 类似。

Java 实现：

```java
public class MyQueue {
    /**
     * 输入栈
     */
    private Stack<Integer> input;
    /**
     * 输出栈
     */
    private Stack<Integer> output;

    /**
     * Initialize your data structure here.
     */
    public MyQueue() {
        input = new Stack<>();
        output = new Stack<>();
    }

    /**
     * Push element x to the back of queue.
     */
    public void push(int x) {
        input.push(x);
    }

    /**
     * Removes the element from in front of queue and returns that element.
     */
    public int pop() {
        if (output.isEmpty()) {
            while (!input.isEmpty()) {
                // 如果输入栈不为空
                output.push(input.pop());
            }
        }

        return output.pop();
    }

    /**
     * Get the front element.
     */
    public int peek() {
        if (input.isEmpty() && output.isEmpty()) {
            return 0;
        }
        if (output.isEmpty()) {
            while (!input.isEmpty()) {
                output.push(input.pop());
            }
        }

        return output.peek();
    }

    /**
     * Returns whether the queue is empty.
     */
    public boolean empty() {
        return input.isEmpty() && output.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

