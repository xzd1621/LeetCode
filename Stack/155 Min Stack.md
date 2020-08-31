#### 155  Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.



**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

 

**Constraints:**

- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.

#### 题目大意

模拟实现栈的push、pop、top和getmin函数。

#### 思路

竟然可以用链表头插法来实现。构造一个链表，包括next、val和minval，在push时构造一个节点，插入到当前首节点之前，并维护minval，在pop时直接将首节点切换到下一个节点，top时直接取出首节点。

#### 代码

```java
class MinStack {

    /** initialize your data structure here. */
    public MinStack() {
        
    }
    
    public void push(int x) {
        LinkNode node = new LinkNode();
        node.next = top;
        node.val = x;
        node.minval = top==null ? x : Math.min(x, top.minval);
        top = node;
    }
    
    public void pop() {
        top = top.next;
    }
    
    public int top() {
        return top.val;
    }
    
    public int getMin() {
        return top.minval;
    }
    
    private static class LinkNode{
        int val;
        int minval;
        LinkNode next;
    }
    private LinkNode top;
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

