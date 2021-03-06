### 只出现一次的数字	LeetCode-136 

##### 题目

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,1]
输出: 1
```

**示例 2:**

```
输入: [4,1,2,1,2]
输出: 4
```

##### 思路

刚刚做过前面那道题（day2-2),很容易就想到设置一个新数组，值为1的就是，但要求线性时间复杂度，还不能使用额外空间，就不能用两层循环套了，放弃这种思路后一直在考虑如何把2个数的消除，但是没有想到好的办法，于是就试了试设置数组的办法可不可行，发现不可以。。在[-1]那里卡住了，改的话有点麻烦，就去google了下解决办法。

以前没有什么使用位运算的经验，看了之后才知道按位异或还可以这样用

- 一个整数与自己异或的结果是0
- 一个整数与0异或的结果是自己
- 异或操作满足交换律，即a^b=b^a

```c
int singleNumber(int* nums, int numsSize) {
    int n = 0;
    for(int i = 0; i < numsSize; i++) {
        n ^= nums[i];
    }
    return n;
}
```