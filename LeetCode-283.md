### 移动零 	LeetCode-283

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
