### 两数之和	LeetCode-1

##### 题目

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

##### 思路

因为只有一种答案，所以我直接用了一个双层循环得到答案返回，n²的时间复杂度果然很慢。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int len = nums.size();
        vector<int> result;
        for(int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                if (i!=j) {
                    if (nums[i] + nums[j] == target) {
                        result.push_back(i);
                        result.push_back(j);
                        return result;
                    }
                }
            }
        }
        return result;
    }
};
```

于是又看了一下前面的算法是怎样的，我大概了解了思路，用target减去数组中的数，放进容器里，再找到数组中相同的答案，把位置记在新的数组中返回即可。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int len = nums.size();
        int a[len] = {1};
        vector<int> result;
        for(int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                if (i!=j) {
                    if (nums[i] + nums[j] == target) {
                        result.push_back(i);
                           result.push_back(j);
                           return result;
                    }
                }
            }
        }
        return result;
    }
};
```