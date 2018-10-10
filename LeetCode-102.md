### LeetCode-102	二叉树的层次遍历

##### 题目

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

##### 思路

用队列来返回每层的结果，每当根节点出队列时，让他的子节点进入队列，在每层开始循环时记住队列里值的个数，循环该次数后即得到每层的结果。

~~~c++
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> tree;
        vector<int> node;
        queue<TreeNode*> s;
        
        int count = 0;
        
        if (root) s.push(root);
        while(!s.empty()) {
            TreeNode* temp;
            node.clear();
            count = s.size();
            for (int i = 0; i < count; i++) {
                temp = s.front();
                s.pop();
                node.push_back(temp->val);
                if (temp->left) {
                    s.push(temp->left);
                }
                if (temp->right) {
                    s.push(temp->right);
                }
            }
            tree.push_back(node);
        }
        return tree;
    }
};
~~~

