#### 82.Remove Duplicates from Sorted List II

Medium

1780110Add to ListShare

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only *distinct* numbers from the original list.

Return the linked list sorted as well.

**Example 1:**

```
Input: 1->2->3->3->4->4->5
Output: 1->2->5
```

**Example 2:**

```
Input: 1->1->1->2->3
Output: 2->3
```

#### 题目大意

将链表中的重复部分都删除，如1->1->1->2->3，删除后则为2->3。

#### 思路

双指针法。首先需设置哑节点便于操作一致，再设置fast节点和slow节点，如果fast.next != null，若fast.next.val != fast.val，那么则说明不重复，fast和slow各前进一步，如果fast.next.val == fast.val，则fast一直前进，直至不等，再fast = fast.next; slow.next = fast，改变slow的指向。

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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode fast = head, slow = dummy;
        while(fast != null && fast.next != null){
            while(fast.next != null && fast.val != fast.next.val){
                fast = fast.next;
                slow = slow.next;
            }
            if(fast.next != null && fast.val == fast.next.val){
                while(fast.next != null && fast.val == fast.next.val){
                fast = fast.next;
                }
                fast = fast.next;
                slow.next = fast;
            }
        }
        return dummy.next;
    }
}
```

