### 反转字符串 	LeetCode-344

##### 题目

编写一个函数，其作用是将输入的字符串反转过来。

**示例 1:**

```
输入: "hello"
输出: "olleh"
```

**示例 2:**

```
输入: "A man, a plan, a canal: Panama"
输出: "amanaP :lanac a ,nalp a ,nam A"
```

##### 思路

从字符串末尾遍历到头赋给新字符串。

```c++
class Solution {
public:
    string reverseString(string s) {
        string result;
        for (int i = s.size()-1; i >= 0; i--) {
            result += s[i];
        }
        return result;
    }
};
```

或者直接使用内置函数reverse

```c++
class Solution {
public:
    string reverseString(string s) {
        reverse(s.begin(),s.end());
        return s;
    }
};
```
