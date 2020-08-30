#### 503  Next Greater Element II

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

**Example 1:**

```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; The number 2 can't find next greater number; The second 1's next greater number needs to search circularly, which is also 2.
```



**Note:** The length of given array won't exceed 10000.

#### 题目大意

给出环形数组，求其右边第一个最大的数。

#### 思路

与I版本不同，该题的数组是环形的，但是思想类似。由于是环形，所以可以将数组扩充为2倍，这样即可完整遍历一次环形。当栈不空并且栈顶的数不大于当前的数时，一直出栈直至没有数大于当前的数，若此时栈为空，则置为-1.否则就是栈顶的数。

#### 代码

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int []res = new int[nums.length];
        Stack<Integer> s = new Stack<Integer>();
        for(int i = 2 * nums.length - 1; i >= 0; i--){
            while(!s.empty() && nums[s.peek()] <= nums[i % nums.length]){
                s.pop();
            }
            res[i % nums.length] = s.empty() ? -1 : nums[s.peek()];
            s.push(i % nums.length);
        }
        return res;
    }
}
```

