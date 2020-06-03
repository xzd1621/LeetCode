#### Add Two Numbers II

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

####题目大意

将链表表示的数字加起来，结果以链表表示

难度：medium

会否：有思路

#### 思路

由于必须逆序取出链表的数字才能加起来，所以可以设置两个栈，分别存储链表，链表尾部数字在栈顶，然后依次取出栈顶数字，若加起来大于10，则进位，最后用头插法逆序构造结果链表。

注意：最后有一位进位时，需要多构造一个节点，比如5+5=10，需要构造节点1,并且链表最后一个节点指向null。

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<Integer>();
        Stack<Integer> s2 = new Stack<Integer>();
        ListNode res = null;
        while(l1 != null){
            s1.push(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            s2.push(l2.val);
            l2 = l2.next;
        }
        int add = 0;
        ListNode newnode;
        while(!s1.empty() || !s2.empty()){
            int top1 = s1.empty() ? 0 : s1.pop();
            int top2 = s2.empty() ? 0 : s2.pop();
            if (add + top1 + top2 > 9)
            {
                newnode = new ListNode(add + top1 + top2 - 10);
                add = 1;
            }
            else
            {
                newnode = new ListNode(add + top1 + top2);
                add = 0;
            }
            newnode.next = res;
            res = newnode;
        }
        if(add > 0)
        {
            newnode = new ListNode(add);
            newnode.next = res;
            res = newnode;
        }
        return res;
    }
}
```

