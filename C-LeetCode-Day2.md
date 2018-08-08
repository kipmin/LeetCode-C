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

##### 解答

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

