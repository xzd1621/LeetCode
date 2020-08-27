#### 19 Remove Nth Node From End of List

Given a linked list, remove the *n*-th node from the end of list and return its head.

**Example:**

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

**Note:**

Given *n* will always be valid.

**Follow up:**

Could you do this in one pass?

#### 题目大意

删除倒数第n个节点，一遍完成

#### 思路

很明显的双指针做法，设置fast和slow两个指针，fast先走n步，然后fast和slow一起走，直到fast.next = null，此时slow.next就是需要删除的倒数第n个节点，直接删除即可。需要注意的是有可能删除第一个节点，所以需要增加哑节点，以便操作一致。这里讲fast和slow都设置为哑节点比较好，因为只要fast先走n再一起走最后删除的节点不变。

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode res = new ListNode(0);
        res.next = head;
        ListNode slow = res, fast = res;
        while(n-- > 0){
            fast = fast.next;
        }
        while(fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        return res.next;
    }
}
```

