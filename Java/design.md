+ [Min Stack](#min-stack)


## Min Stack

https://leetcode.com/problems/min-stack/

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.

pop() -- Removes the element on top of the stack.

top() -- Get the top element.

getMin() -- Retrieve the minimum element in the stack.
 

Example:
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

```java
class MinStack {
    Stack<Integer> stack = new Stack<>();
    Stack<Integer> minStack = new Stack<>(); // keeps track of minimums

    // Always push onto stack. If it's a minimum, also push it onto minStack
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= getMin()) {
            minStack.push(x);
        }
    }

    // Pop off stack. If we popped a minimum, we remove it from minStack also
    public void pop() {
        if (stack.isEmpty()) {
            return;
        }
        int x = stack.pop();
        if (x == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```
or
```java
 class MinStack {

        private class Entry {
            int value;
            Entry previous;
            int min;

            public Entry(int value, Entry entry) {
                this.value = value;
                this.previous = entry;
            }
        }

        Entry top;

        public MinStack() {
        }

        public void push(int x) {
            Entry current = new Entry(x, top);
            current.min = (top != null && top.min < current.value) ? top.min : current.value;
            top = current;
        }

        public void pop() {
            top = top.previous;
        }

        public int top() {
            return top.value;
        }

        public int getMin() {
            return top.min;
        }
    }
```
