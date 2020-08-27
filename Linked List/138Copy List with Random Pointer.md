#### 138 Copy List with Random Pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list.

The Linked List is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) where random pointer points to, or `null` if it does not point to any node.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```

**Example 3:**

**![img](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```

**Example 4:**

```
Input: head = []
Output: []
Explanation: Given linked list is empty (null pointer), so return null.
```

 

**Constraints:**

- `-10000 <= Node.val <= 10000`
- `Node.random` is null or pointing to a node in the linked list.
- Number of Nodes will not exceed 1000.

#### 题目大意

深拷贝链表，链表包括next指针和random指针。

#### 思路

想破脑袋也想不出这种做法。利用hashmap，key是原链表上的节点，value是我们用原链表节点的val构造出来的新节点，这样遍历完之后相当于拷贝了原链表的所有节点的值，接着再遍历一遍来拷贝其指针，hashmap的value.next就是key.next的value，对于random指针亦是如此，所以可以用m.get(tmp).next = m.get(tmp.next);

需要注意hashmap取值和置值得方式是m.get和m.put。

#### 代码

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node, Node> m = new HashMap<>();
        Node tmp = head;
        while(tmp != null){
            m.put(tmp, new Node(tmp.val));
            tmp = tmp.next;
        }
        tmp = head;
        while(tmp != null){
            m.get(tmp).next = m.get(tmp.next);
            m.get(tmp).random = m.get(tmp.random);
            tmp = tmp.next;
        }
        return m.get(head);
    }
}
```

