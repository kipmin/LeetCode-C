### 存在重复	LeetCode-217 

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
