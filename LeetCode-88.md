### LeetCode-88	合并两个有序数组

##### 题目

给定两个有序整数数组 *nums1* 和 *nums2*，将 *nums2* 合并到 *nums1* 中*，*使得 *num1* 成为一个有序数组。

**说明:**

- 初始化 *nums1* 和 *nums2* 的元素数量分别为 *m* 和 *n*。
- 你可以假设 *nums1* 有足够的空间（空间大小大于或等于 *m + n*）来保存 *nums2* 中的元素。

**示例:**

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

##### 思路

vector可以较为方便的在中间增删数据，所以我通过比较两个数组，发现s2中较大的就放在s1标志的后面，再通过s1+已添加数据的个数，知道s1有效数据结尾的地方，然后把s2中剩余的数据都输入进去。

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) { 
        int temp = 0;
        for (int i = 0; i < m+n; i++) {
            if (temp == n) break;
            if (i-temp == m) {
                nums1.insert(nums1.begin()+m+temp, nums2[temp]);
                nums1.pop_back();
                temp++;
            } else if ( nums1[i] > nums2[temp]) {
                nums1.insert(nums1.begin()+i, nums2[temp]);
                nums1.pop_back();
                temp++;
            }
        }
    }
};
```

