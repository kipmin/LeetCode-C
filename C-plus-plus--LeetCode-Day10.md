---
title: LeetCode-Day9
date: 2018-09-05 12:00:00
tags:
---

### LeetCode-38 报数

##### 题目

报数序列是指一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` 被读作  `"one 1"`  (`"一个一"`) , 即 `11`。
`11` 被读作 `"two 1s"` (`"两个一"`）, 即 `21`。
`21` 被读作 `"one 2"`,  "`one 1"` （`"一个二"` ,  `"一个一"`) , 即 `1211`。

给定一个正整数 *n* ，输出报数序列的第 *n* 项。

注意：整数顺序将表示为一个字符串。

**示例 1:**

```
输入: 1
输出: "1"
```

**示例 2:**

```
输入: 4
输出: "1211"
```

##### 思路

递归求解，设置两个指针，后面的指针依次+1，跟前面的指针作比较，碰到不同的数就在字符串后加该数出现的次数，以及这个数。

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    return 0;
}();

class Solution {
public:
    string countAndSay(int n) {
        string str,temp;
        int a,b;
        if (n == 1) {
            return "1";
        } else {
            temp = countAndSay(n-1);
            for (int i = 0,j = 1; j <= temp.size(); j++) {
                if (temp[i] != temp[j]) {
                    str += (j-i+'0');
                    str += temp[i];
                    i = j;
                }
            }
            return str;
        }
        
        
    }
};
```



### LeetCode-14 最长公共前缀

##### 题目

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1:**

```
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例 2:**

```
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

**说明:**

所有输入只包含小写字母 `a-z` 。

##### 思路

将数组中的字符串依次跟第一个字符串比较，留下跟第一个字符串相同的部分。

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    return 0;
}();

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int n, i = 0, len = INT_MAX;
        if (strs.empty()) return "";
        string str = strs[0];
        for (string s : strs) {
            if (s.empty()) return "";
            i = 0;
            while ( str[i] == s[i] ) {
                    i++;
                if (i == str.size() || i == s.size()) break;
            }
            if (i != str.size()) 
                str.erase(str.begin()+i,str.end());
        }
        return str;
    }
};
```

