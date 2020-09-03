#### 1190  Reverse Substrings Between Each Pair of Parentheses

You are given a string `s` that consists of lower case English letters and brackets. 

Reverse the strings in each pair of matching parentheses, starting from the innermost one.

Your result should **not** contain any brackets.

 

**Example 1:**

```
Input: s = "(abcd)"
Output: "dcba"
```

**Example 2:**

```
Input: s = "(u(love)i)"
Output: "iloveu"
Explanation: The substring "love" is reversed first, then the whole string is reversed.
```

**Example 3:**

```
Input: s = "(ed(et(oc))el)"
Output: "leetcode"
Explanation: First, we reverse the substring "oc", then "etco", and finally, the whole string.
```

**Example 4:**

```
Input: s = "a(bcdefghijkl(mno)p)q"
Output: "apmnolkjihgfedcbq"
```

 

**Constraints:**

- `0 <= s.length <= 2000`
- `s` only contains lower case English characters and parentheses.
- It's guaranteed that all parentheses are balanced.

#### 题目大意

括号里的字符串逆序，递归操作。

#### 思路

遇到字符串类型的还是stringbuilder好使，再加上一个存储字符串的栈。遇到(将已构造的字符串进栈，并将字符串置空，遇到字符则一直连接构造字符串，遇到)就将当前的字符串反转，并将栈顶的字符串连接在该反转后的字符串之前。

#### 代码

```java
class Solution {
    public String reverseParentheses(String s) {
        Stack<String> ans = new Stack<String>();
        StringBuilder sb = new StringBuilder();
        for(char c : s.toCharArray()){
            if(c == '('){
                ans.push(sb.toString());
                sb = new StringBuilder();
            }
            else if(c == ')'){
                sb = sb.reverse();
                sb.insert(0, ans.pop());
            }
            else{
                sb.append(c);
            }
        }
        return sb.toString();
    }
}
```

