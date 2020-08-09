#### 147.Insertion Sort List

- Sort a linked list using insertion sort.

  

  ![img](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
  A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
  With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list

  **Algorithm of Insertion Sort:**

  1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
  2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
  3. It repeats until no input elements remain.

  
  **Example 1:**

  ```
  Input: 4->2->1->3
  Output: 1->2->3->4
  ```

  **Example 2:**

  ```
  Input: -1->5->3->4->0
  Output: -1->0->3->4->5
  ```

#### 题目大意

将链表进行插入排序。

#### 思路

主要就是插入排序的思想，将链表分为待排序部分和已排序部分，每次取出待排序部分的头节点，依次遍历已排序部分，找到这样一个节点，它的值比待排序头节点的值小，其后一个节点的值比待排序的头节点大，将该节点插入。需要注意的是，同样需要设置一个头节点，以便在第一个节点前插入时操作一致。

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
    public ListNode insertionSortList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode tail = head, sort = head.next; //已排序的最后一个节点和未排序的首节点
        while(sort != null){
            if(sort.val < tail.val){
                ListNode tmp = dummy;
                while(tmp.next.val < sort.val)
                    tmp = tmp.next;
                tail.next = sort.next;
                sort.next = tmp.next;
                tmp.next = sort;
                sort = tail.next;
            }
            else{
                sort = sort.next;
                tail = tail.next;
            }
        }
        return dummy.next;
    }
}
```

