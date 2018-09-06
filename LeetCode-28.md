### LeetCode-28	实现strStr() 

##### 题目

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。

##### 思路

这个题关键在于有多个重复部分的词如何解决，比如ississic,issic,需要在两个字符串比较的时候，碰到不同就回退j个位置。

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    int strStr(string haystack, string needle) {
        if (needle.empty())
            return 0;
        int i = 0, j = 0;
        while(i < haystack.size() && j < needle.size()) {
            if (haystack[i] == needle[j]) {
                i++;
                j++;
            } else {
                i++;
                if (j != 0) {
                    i -= j;
                    j = 0;
                }
            }
        }
        if (j == needle.size()){
            return i-j;
        } else {
            return -1;
        }
    }
};
```
