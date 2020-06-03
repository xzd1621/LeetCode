#### 725 Split Linked List in Parts

Given a (singly) linked list with head node `root`, write a function to split the linked list into `k` consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

**Example 1:**

```
Input:
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].
```



**Example 2:**

```
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```



**Note:**

The length of `root` will be in the range `[0, 1000]`.

Each value of a node in the input will be an integer in the range `[0, 999]`.

`k` will be an integer in the range `[1, 50]`.

#### 题目大意

分割链表，将链表分成k段，每段长度相差不能超过1，若不能均分，则将长的段都分在前面。

#### 思路

先计算分几段，能不能均分，首先计算sec=length/k，其中前length%k段的长度为sec + 1，后面的长度为sec。由于直接利用之前的链表来构造结果时，会涉及到链表的断开问题，所以可以重新构造链表，可以使用ListNode node = new ListNode(0);的方法来构造一个头节点，便于插入，最后返回时直接返回node.next即可。

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
    public ListNode[] splitListToParts(ListNode root, int k) {
        ListNode tmp = root;
        int length = 0;
        while(tmp != null)
        {
            length++;
            tmp = tmp.next;
        }
        int sec = length / k, rem = length % k;
        ListNode[] res = new ListNode[k];
        tmp = root ;
        for(int i = 0; i < k; i++)
        {
            ListNode head = new ListNode(0), ele = head;
            for(int d = 0; d < sec + (i < rem ? 1 : 0); d++)
            {
                head.next = new ListNode(tmp.val);
                head = head.next;
                if (tmp != null) tmp = tmp.next;
            }
            res[i] = ele.next;
        }
        return res;
    }
}
```

