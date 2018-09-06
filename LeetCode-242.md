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