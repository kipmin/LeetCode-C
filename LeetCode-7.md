### 颠倒整数	LeetCode-7

##### 题目

给定一个 32 位有符号整数，将整数中的数字进行反转。

**示例 1:**

```
输入: 123
输出: 321
```

 **示例 2:**

```
输入: -123
输出: -321
```

**示例 3:**

```
输入: 120
输出: 21
```

**注意:**

假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。根据这个假设，如果反转后的整数溢出，则返回 0。

##### 思路

因为这个章节是字符串嘛，所以就想到用字符串来颠倒，可是c++的这个try catch跟java的不太一样，一直提示报错，就只好用以前的思路了，下面这个一直提示报错的大家看看就好。

```c++
class Solution {
public:
    int reverse(int x) {
        bool b = true;
        int num = 0;
        if (x < 0) {
            b = false;
            x = -x;
        }
        string s = to_string(x);
        string str;
        for (int i = s.size()-1; i >= 0; i--) {
            str += s[i];
        }
        try {
            num = std::stoi(str);
        } catch (const std::invalid_argument& e) {
            return 0;
        }
        if(!b) num = -num;
        return num;
    }
};
```

最后的出错信息

```c++
执行出错信息：
terminate called after throwing an instance of 'std::out_of_range'
  what():  stoi
最后执行的输入：
1534236469
```

这个是通过提交的正常解法。

```c++
class Solution {
public:
    int reverse(int x) {
        int n = 0;
        int temp = 0;
        while(x) {
            temp = temp*10 + x%10;
            if (temp/10 != n) {
                return 0;
            }
            n = temp;
            x /= 10;
        }
        return n;
    }
};
```