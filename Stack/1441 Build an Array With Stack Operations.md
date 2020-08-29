#### 1441 Build an Array With Stack Operations

Given an array `target` and an integer `n`. In each iteration, you will read a number from  `list = {1,2,3..., n}`.

Build the `target` array using the following operations:

- **Push**: Read a new element from the beginning `list`, and push it in the array.
- **Pop**: delete the last element of the array.
- If the target array is already built, stop reading more elements.

You are guaranteed that the target array is strictly increasing, only containing numbers between 1 to `n` inclusive.

Return the operations to build the target array.

You are guaranteed that the answer is unique.

 

**Example 1:**

```
Input: target = [1,3], n = 3
Output: ["Push","Push","Pop","Push"]
Explanation: 
Read number 1 and automatically push in the array -> [1]
Read number 2 and automatically push in the array then Pop it -> [1]
Read number 3 and automatically push in the array -> [1,3]
```

**Example 2:**

```
Input: target = [1,2,3], n = 3
Output: ["Push","Push","Push"]
```

**Example 3:**

```
Input: target = [1,2], n = 4
Output: ["Push","Push"]
Explanation: You only need to read the first 2 numbers and stop.
```

**Example 4:**

```
Input: target = [2,3,4], n = 4
Output: ["Push","Pop","Push","Push","Push"]
```

 

**Constraints:**

- `1 <= target.length <= 100`
- `1 <= target[i] <= 100`
- `1 <= n <= 100`
- `target` is strictly increasing.

#### 题目大意

给出一个数组和n，要求对从1到n的数字进行push和pop操作，得到给出的数组。

#### 思路

可以来模拟这个过程，设置i从1到n开始遍历，设置m=0，先直接将元素进栈，依次将i与target[m]比较，若i==target[m]，则指向下一个target的元素，m++，若不等，则出栈。需要注意的是，若target遍历完则退出循环。

#### 代码

```java
class Solution {
    public List<String> buildArray(int[] target, int n) {
        List<String> res = new ArrayList<>();
        int m = 0;
        for(int i = 1; i <= n && m < target.length; i++){
            res.add("Push");
            if(i == target[m]){
                m++;
            }
            else{
                res.add("Pop");
            }
        }
        return res;
    }
}
```

