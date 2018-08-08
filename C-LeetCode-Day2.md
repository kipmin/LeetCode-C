---
title: LeetCode-Day2
date: 2018-08-08 12:00:00
tags:
---

### 旋转数组

#####  题目

给定一个数组，将数组中的元素向右移动 *k* 个位置，其中 *k* 是非负数。

**示例 1:**

```c
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```c
输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

**说明:**

- 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
- 要求使用空间复杂度为 O(1) 的原地算法。

##### 思路

我刚开始的想法是跟着解释来的，而且我理解的原地算法就是只能用原数组，好吧，底下这个是我刚开始的思路，就是通过保留最后一个数，将其余都向右挪一位，再把最后一个数放最前面的方法，k是几，就旋转几次，说的很明白了，看代码吧

```c
void rotate(int* nums, int numsSize, int k) {
    int i, temp;
    for(k;k>0;k--) {
        temp = nums[numsSize-1];
        for(i = numsSize-2; i >= 0; i--) {
            nums[i+1] = nums[i];
        }
        nums[0] = temp;
    }
}
```

通过解答之后。。344ms。。。看了看前面的算法，好吧，这个省了空间好像没啥意义，而且4ms的样例让我get了一个memcpy的用法，虽然没什么用吧，但还是挺开心的。底下是用空间换时间的思路，把需要旋转的数取出来，将其他数都挪好位置，再利用memcpy函数把数组拼接起来，实际上是替换了第一个参数中的选定长度内存地址中的内容，func2()。

```c
void rotate(int* nums, int numsSize, int k) {
    // func1(nums, numsSize, k);
    func2(nums, numsSize, k);
}

// void func1(int* nums, int numsSize, int k) {
//     int i, temp;
//     for(k;k>0;k--) {
//         temp = nums[numsSize-1];
//         for(i = numsSize-2; i >= 0; i--) {
//             nums[i+1] = nums[i];
//         }
//         nums[0] = temp;
//     }
// }

void func2(int* nums, int numsSize, int k) {
    k=k%numsSize;
    int* a = (int*)malloc(sizeof(int)*k);
    for (int i = 0; i < k; i++) {
        a[i] = nums[numsSize-k+i];
    }
    for (int i = numsSize-k-1; i >= 0; i--) {
        nums[i+k] = nums[i];
    }
    memcpy(nums, a, sizeof(int)*k);
}
```

### 存在重复 

##### 题目

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

**示例 1:**

```
输入: [1,2,3,1]
输出: true
```

**示例 2:**

```
输入: [1,2,3,4]
输出: false
```

**示例 3:**

```
输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

##### 思路

刚开始是用2层循环的办法，如果把这个当成一个大表格，我就遍历了其中的一个倒三角，时间复杂度应该是n²？发现果然不行。。时间超限，就想到最前面做的那道排序数组中删除重复项，就先把数组排了个序，c语言没有写好的排序算法，就用了qsort，排好序之后就和第一道题一样的思路了（day1-1）

```c
int comp(const void *a, const void *b) {
    return *(int *)a-*(int *)b;
}

bool containsDuplicate(int* nums, int numsSize) {
    if (numsSize < 2) {
        return false;
    }
    qsort(nums, numsSize, sizeof(int), comp);
    for (int i = 0; i < numsSize-1; i++) {
        if (nums[i] ==nums[i+1]) {
            return true;
        }
    }
    return false;
}

```

先排序再查重的办法直接拿到了12ms的成绩，于是看了看前面8ms的是怎么做的，这个思路真的很厉害了，先得到数组中最小的一个数，再用整个数组来减这个最小的数，如果有2个差是相同的值就说明有重复的数。

```c
bool containsDuplicate(int* nums, int numsSize) {
    if (numsSize < 2) {
        return false;
    }
    int min = 0;
    for (int i = 0; i < numsSize; i++) {
        min = min > nums[i]?nums[i]:min;
    }
    int index[999999] = {0};
    for (int i = 0; i < numsSize; i++) {
        if (index[nums[i]-min] != 0) {
            return true;
        }
        index[nums[i]-min]++;
    }
    return false;
}
```

