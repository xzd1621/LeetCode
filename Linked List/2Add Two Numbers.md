#### 2 Add Two Numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

#### 题目大意

两个链表相加，生成的结果也用链表表示

#### 思路

与Add Two Numbers II类似，只不过这个加起来之后往后进位，而II是往前进位，所以本题可以使用尾插法建立链表，而II需要用栈保存之后用头插法建立链表。同样需要注意6+4 = 10这种情况。

头插法：

```java
ListNode res = null;
while(...){
    ListNode ans = new ListNode(num);
    ans.next = res;
    res = ans;
}
return res;
```

最后构造的链表是数字的逆序

尾插法：

```java
ListNode L = new ListNode(0), res = L;
while (...){
ListNode ans = new ListNode(num);
L.next = ans;
L = L.next;
}
return res.next; 
```

#### 代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode res = new ListNode(0), res_l = res;
        int add = 0;
        while(l1 != null || l2 != null){
            int a = l1 == null ? 0 : l1.val;
            int b = l2 == null ? 0 : l2.val;
            ListNode ans;
            if(a + b + add > 9){
                ans = new ListNode(a + b + add - 10);
                add = 1;
                res.next = ans ;
                res = res.next;
            }
            else{
                ans = new ListNode(a + b + add);
                add = 0;
                res.next = ans ;
                res = res.next;
            }
            if(l1 != null) l1 = l1.next;
            if(l2 != null) l2 = l2.next;
        }
        if (add > 0)
        {
            res.next = new ListNode(1);
        }
        return res_l.next;
    }
}
```

