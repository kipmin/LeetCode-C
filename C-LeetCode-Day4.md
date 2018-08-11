---
title: LeetCode-Day3
date: 2018-08-11 12:00:00
tags:
---

### 加一 

##### 题目

给定一个**非负整数**组成的**非空**数组，在该数的基础上加一，返回一个新的数组。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

**示例 1:**

```
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
```

**示例 2:**

```
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

##### 思路

思路是从后往前遍历，碰到9就计数，并把9改成0，直到一个不是9的数，将其加一，就好了

发现有个示例没通过，是没考虑9,99,999这种情况，于是判断下首位是不是0，是的话就把首位改成1再在末尾加0就ok了。

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for (int i = digits.size()-1; i >= 0; i--) {
            if (digits[i] == 9) {
                digits[i] = 0;
            } else {
                digits[i]++;
                break;
            }
        }
        if (digits[0] == 0) {
            digits[0] = 1;
            digits.push_back(0);
        }
        return digits;
    }
};
```

### 移动零 

##### 题目

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例:**

```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**说明**:

1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。

##### 思路

通过遍历，在移动0的过程中，碰到后方的0，使交换的数字的间隔+1，没碰到后方的0，就交换数字，这样遍历一遍就把所有的0放在了数组最后面。

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int a = 1;
        if(nums.size() > 1 ) {
            for (int i = 0; i <nums.size(); i++) {
                if (nums[i] == 0) {
                    if (nums[i+a] != 0) {
                        nums[i] ^= nums[i+a];
                        nums[i+a] ^= nums[i];
                       	nums[i] ^= nums[i+a];
                   } else {
                       a++;
                       i--; //保证是第一个0和最后一个0后面的数做交换
                   }
                } 
                if (i+a+1 == nums.size())
                    break; //循环结束后跳出
            }
        }
    }
};
```

看了看比我时间短的两种代码，都是一个思路，遇到0直接跳过，把所有非0的数排在一起，等最后在尾巴上加0，挑了一个思路简洁清晰的重写了一遍

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int len = nums.size();
        int j = 0;
        for (int i = 0; i < len; i++) {
            if (nums[i] != 0) {
                nums[j] = nums[i];
                j++;
            }
        }
        for (;j < len;j++) {
            nums[j] = 0;
        }
    }
};
```

