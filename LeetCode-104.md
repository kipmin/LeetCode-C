### LeetCode-104	二叉树的最大深度 

##### 题目

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

##### 思路

很简单的递归

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
static int x = []() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    return 0;
}();

class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root) return 0;
        int maxL = 0,maxR = 0;
        if (root->left) {
            maxL = maxDepth(root->left);
        }
        if (root->right) {
            maxR = maxDepth(root->right);
        }
        return max(maxL,maxR)+1;
    }
};
```

