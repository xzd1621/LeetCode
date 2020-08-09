#### 1171. Remove Zero Sum Consecutive Nodes from Linked List

Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list. You may return any such answer.

 

(Note that in the examples below, all sequences are serializations of `ListNode` objects.)

**Example 1:**

```
Input: head = [1,2,-3,3,1]
Output: [3,1]
Note: The answer [1,2,1] would also be accepted.
```

**Example 2:**

```
Input: head = [1,2,3,-3,4]
Output: [1,2,4]
```

**Example 3:**

```
Input: head = [1,2,3,-3,-2]
Output: [1]
```

 

**Constraints:**

- The given linked list will contain between `1` and `1000` nodes.
- Each node in the linked list has `-1000 <= node.val <= 1000`.

#### 题目大意

将链表中连续和为0的部分去掉。

#### 思路

主要是前缀和思想和map，首先需设置一个虚拟的头节点指向第一个节点。

##### 思路1

首先依次计算首节点到第i个节点之间的和（包括第i个），并存入hashmap中，键为前缀和，值为节点，每次计算完前缀和之后，看当前的hashmap中是否有该前缀和对应的节点，如果有，则说明存在a1+……+am = a1+……+am+……+an = prefix，则a(m+1) + ……+an = 0，可将这部分为0的删除，同时需要注意将这部分前缀和的hashmap删除。删除过程：首先根据hashmap获取到m节点，再往后遍历，遍历过程中 prefix += i.val，直至prefix又回到之前的值，并且边遍历便删除hashmap的key，遍历完成之后再用m.get(prefix).next = tmp.next改变指针位置。

##### 思路2

遍历两次，首次计算前缀和，因为前缀和相同时，m.put(prefix, node)，会将后面prefix相同的覆盖掉前面的，所以m.get(prefix)会得到之后前缀和为prefix的节点。那么第二次遍历时，同样计算前缀和，每次遍历一个节点时，i.next = m.get(prefix).next，若不存在前缀和相同的两个节点，则m.get(prefix) = i，语句无影响，若存在，则m.get(prefix)是后面一个前缀和为prefix的节点，直接断链。

#### 代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeZeroSumSublists(ListNode head) {
        
        //solution 1
        ListNode dummy = new ListNode(0), cur = dummy;
        dummy.next = head;
        Map<Integer, ListNode> m = new HashMap<>();
        int prefix = 0; //前缀和
        while(cur != null){
            prefix += cur.val;
            if(m.containsKey(prefix)){
                ListNode tmp = m.get(prefix).next;
                int p = prefix + tmp.val;
                while(p != prefix){
                    m.remove(p);
                    tmp = tmp.next;
                    p += tmp.val;
                }
                m.get(prefix).next = tmp.next;
              //  cur = tmp.next;
            }
            else{
                m.put(prefix, cur);
            }
            cur = cur.next;
        }
        return dummy.next;
    
        //solution 2
        ListNode dummy = new ListNode(0), cur = dummy;
        dummy.next = head;
        Map<Integer, ListNode> m = new HashMap<>();
        int prefix = 0;
        while(cur != null){
            prefix += cur.val;
            m.put(prefix, cur);
            cur = cur.next;
        } 
        prefix = 0;
        for(ListNode i = dummy; i != null; i = i.next){
            prefix += i.val;
            i.next = m.get(prefix).next;
        }
        return dummy.next;
    }
}
```

