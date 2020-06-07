#### 92 Reverse Linked List II

Reverse a linked list from position *m* to *n*. Do it in one-pass.

**Note:** 1 ≤ *m* ≤ *n* ≤ length of list.

**Example:**

```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

#### 题目大意

将链表从m到n的部分进行反转，一遍完成。

#### 思路

这题好难，不会啊。

首先用一个res保存最后的结果的头节点，由于可能从第一个就开始反转，所以用res.next = head，以便之后操作方便，不用判断是否是头节点。从m+1个位置开始到第n个位置，每次都是将当前节点插入到m-1位置之后，再连接第m个节点，类似于头插法可以逆序构造链表。需要注意用pre保存第m-1个位置，类似于头插法的头节点。

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode res = new ListNode(0), pre = res;
        res.next = head;
        for(int i = 0; i < m - 1; i++)
            pre = pre.next;
        ListNode cur = pre.next;
        for(int i = m; i < n; i++)
        {
            ListNode tmp = cur.next;
            cur.next = tmp.next;
            tmp.next = pre.next;
            pre.next = tmp;
        }
        return res.next;
    }
}
```

