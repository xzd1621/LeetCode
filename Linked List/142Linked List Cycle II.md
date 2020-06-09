#### 142 Linked List Cycle II

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Note:** Do not modify the linked list.

 

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**Follow-up**:
Can you solve it without using extra space?

#### 题意

与Linked List Cycle类似，只不过这道题要求寻找环的首节点。若不存在环，则返回null

#### 思路

与之前的题目思路大致相同，也是采用双指针法，设置快慢指针，快指针每次走两步，慢指针走一步，最后重合时快指针比慢指针多走一圈，不会跳过是因为快指针追慢指针，每次距离缩小1，最后减至0。此时，快指针走的距离恰好是慢指针的2倍，所以，慢指针走的距离就是1圈，因此从首节点到环的开始节点的距离+环开始节点到相遇点的距离=环1圈的长度，所以相遇点到环开始节点的距离（顺时针方向）=首节点到环的开始节点的距离，可以再设置双指针，一个从首节点走，一个从相遇节点走，速度一样，相遇位置就是环的开始节点。

#### 代码

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head == null || head.next == null) return null;
        ListNode fast = head, slow = head;
        while(fast != null && fast.next != null)
        {
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow) break;
        }
        if(fast == null || fast.next == null) return null;
        slow = head;
        while(fast != slow)
        {
            fast = fast.next;
            slow = slow.next;
        }
        return fast;
    }
}
```

