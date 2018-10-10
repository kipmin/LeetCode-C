### LeetCode-108	将有序数组转换为二叉搜索树

##### 题目

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

##### 思路

观察示例提供的答案数组，发现每个根节点都是在最深左子节点和最深又子节点中间，可以用递归的方式求解。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        TreeNode* a = nullptr;
        if (nums.empty()) {
            return a;
        } else {
            int count = nums.size();
            return sortedArrayToBST(nums, 1, (1+count)/2, count);
        }
    }
    
    TreeNode* sortedArrayToBST(vector<int>& nums, int left, int mid, int right) {
        if (left == right) return new TreeNode(nums[left-1]);
        if (left+1 == right) {
            TreeNode* num = new TreeNode(nums[left-1]);
            num->right = sortedArrayToBST(nums, left+1, (left+right)/2, right);
            return num;
        }
        TreeNode* root = new TreeNode(nums[mid-1]);
        root->left = sortedArrayToBST(nums, left, (left+mid-1)/2, mid-1);
        root->right = sortedArrayToBST(nums, mid+1, (mid+1+right)/2, right);
        return root;
    }
};
```

