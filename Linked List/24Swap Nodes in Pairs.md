#### 24 Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

 

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

#### 题目大意

给出一个链表，将链表的每两个片段反转一下

#### 思路

递归。若链表为空或者只有一个节点，则不做任何操作，否则，后面n-2个节点使用递归算法生成即可，最后再调整这三部分的位置。

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
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode res = head.next;
        res.next = swapPairs(res.next);
        head.next = res.next;
        res.next = head;
        return res;
    }
}
```

