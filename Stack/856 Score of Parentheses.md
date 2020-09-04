#### 856 Score of Parentheses

Given a balanced parentheses string `S`, compute the score of the string based on the following rule:

- `()` has score 1
- `AB` has score `A + B`, where A and B are balanced parentheses strings.
- `(A)` has score `2 * A`, where A is a balanced parentheses string.

 

**Example 1:**

```
Input: "()"
Output: 1
```

**Example 2:**

```
Input: "(())"
Output: 2
```

**Example 3:**

```
Input: "()()"
Output: 2
```

**Example 4:**

```
Input: "(()(()))"
Output: 6
```

 

**Note:**

1. `S` is a balanced parentheses string, containing only `(` and `)`.
2. `2 <= S.length <= 50`

#### 题目大意

计算得分，()分数为1，AB得分为A+B, (A)得分为2*A

#### 思路

只需要计算每层()之外有几层即可，有k层，则得分为2^k，累计求和就行。

#### 代码

```java
class Solution {
    public int scoreOfParentheses(String S) {
        int l = 0, res = 0;
        for(int i = 0; i < S.toCharArray().length; i++){
            if(S.toCharArray()[i] == '('){
                l++;
            }
            else{
                if(S.toCharArray()[i - 1] == '(')
                res += 1 << (l - 1);
                l--;
            }
        }
        return res;
    }
}
```

