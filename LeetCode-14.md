### LeetCode-14 	最长公共前缀

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