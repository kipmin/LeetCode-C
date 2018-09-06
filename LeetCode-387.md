### 字符串中的第一个唯一字符 	LeetCode-387

##### 题目

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

 

**注意事项：**您可以假定该字符串只包含小写字母。

##### 思路

之前常常有疑问，那些速度特别快的算法前面总有几句结构体不知道是啥，今天查了一下

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();
```

###### sync_with_stdio

这个函数是一个“是否兼容stdio”的开关，C++为了兼容C，保证程序在使用了std::printf和std::cout的时候不发生混乱，将输出流绑到了一起。 

###### cin.tie(NULL)

在默认的情况下cin绑定的是cout，每次执行 << 操作符的时候都要调用flush，这样会增加IO负担。可以通过tie(0)（0表示NULL）来解除cin与cout的绑定，进一步加快执行效率。 

全部是小写字母容易很多，直接把字符串遍历一遍，将字符的次数保存到数组，再重新遍历，碰到的第一个值为1的就是了。

```c++
static int xx = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    int firstUniqChar(string s) {
        int r[26] = {0};
        int a;
        for (int i = 0; i < s.size(); i++) {
            a = s[i]-'a';
            r[a]++;
        }
        for (int i = 0; i < s.size(); i++) {
            a = s[i]-'a';
            if (r[a] == 1) {
                return i;
            }
        }
        return -1;
    }
};
```
