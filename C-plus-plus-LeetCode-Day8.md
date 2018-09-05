---
title: C-plus-plus-LeetCode-Day8
date: 2018-08-19 12:00:00
tags:
---

### 有效的字母异位词 	LeetCode-242

##### 题目

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的一个字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

**说明:**
你可以假设字符串只包含小写字母。

**进阶:**
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

##### 思路

先对字符串进行排序，然后按位比较是否相同

```c++
static int xx = [](){
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        int i = 0;
        while(s[i] || t[i]) {
            if ( s[i] != t[i]) {
                return false;
            }
            i++;
        }
        return true;
    }
};
```

或者老办法，设置2个数组存每个字母出现的次数，再比较出现的次数是否相同

```c++
static int xx = [](){
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    bool isAnagram(string s, string t) {
        int a[26]{},b[26]{};
        for(auto temp : s) {
            a[temp-'a']++;
        }
        for(auto temp : t) {
            b[temp-'a']++;
        }
        for (int i = 0; i < 26; i++)
            if (a[i] != b[i])
                return false;
        return true;
    }
};
```

### 验证回文字符串	LeetCode-125

##### 题目

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**

```
输入: "race a car"
输出: false
```

##### 思路

这个破题浪费了我好多时间。。先是忘了回文串是啥，做错了好多遍，再之后又碰到个想死的越界问题，突然觉得java好好，越界都有提醒的。

思路主要是将输入的字符串简化，大写字母变小写，最后只剩下小写字母和数字，然后反转字符串和原字符串比较，相同就说明是回文串。

我如果用reverse就没有那个该死的越界qwq，~~让你自己手写~~

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    bool isPalindrome(string s) {
        string a, b;
        int i = 0;
        for (auto temp : s) {
            if (temp >= 'a' && temp <= 'z') {
                a += temp;
                i++;
            } else if (temp >= 'A' && temp <= 'Z') {
                a += temp+32;
                i++;
            } else if (temp >= '0' && temp <= '9') {
                a += temp;
                i++;
            }
        }
        i--; //就是这个地方，越界了，我自己调试的时候2个字符串看上去也没区别。
        for (; i >= 0; i--) {
            b += a[i];
        }
        if (a == b) {
            return true;
        } else {
            return false;
        }
    }
};
```

