+ [Min Stack](#min-stack)


## Min Stack

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
    ArrayList<Integer> list = new ArrayList<Integer>();
    public MinStack() {    
    }    
    public void push(int x) {
             list.add(x);        
    }
    
    public void pop() {
        list.remove(list.size()-1);        
    }
    
    public int top() {
        if(list.size() >0)
            return list.get(list.size()-1);
        
        return 0;
        
    }
    
    public int getMin() {
        return Collections.min(list);
    }
}
```