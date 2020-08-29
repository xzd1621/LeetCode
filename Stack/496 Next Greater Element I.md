#### 496  Next Greater Element I

You are given two arrays **(without duplicates)** `nums1` and `nums2` where `nums1`’s elements are subset of `nums2`. Find all the next greater numbers for `nums1`'s elements in the corresponding places of `nums2`.

The Next Greater Number of a number **x** in `nums1` is the first greater number to its right in `nums2`. If it does not exist, output -1 for this number.

**Example 1:**

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```



**Example 2:**

```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```



**Note:**

1. All elements in `nums1` and `nums2` are unique.
2. The length of both `nums1` and `nums2` would not exceed 1000.

#### 题目大意

给出两个数组，nums1是nums2的子数组，求nums1的每个元素在nums2的下一个比它大的数。

#### 思路

单调栈的思想。将nums2的数自右向左依次入栈，当栈不空并且当前数比栈顶数大时，依次出栈，直至遇到比它大的，若无，则置为-1，用hashmap保存结果，键为nums2[i]，值为右边第一个比它大的。最后直接查找hashmap即可得到最终结果。

#### 代码

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> m = new HashMap<>();
        Stack<Integer> s = new Stack<>();
        for(int i = nums2.length - 1; i >= 0; i--){
            while(!s.empty() && s.peek() < nums2[i]){
                s.pop();
            }
            if(s.empty()){
                m.put(nums2[i], -1);
            }
            else{
                m.put(nums2[i], s.peek());
            }
            s.push(nums2[i]);
        }
        for(int i = 0; i < nums1.length; i++){
            nums1[i] = m.get(nums1[i]);
        }
        return nums1;
    }
}
```

