### LeetCode-101	对称二叉树

##### 题目

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

**说明:**

如果你可以运用递归和迭代两种方法解决这个问题，会很加分。

##### 思路

###### 递归

因为是对称的二叉树，把左子树的左值跟右子树的右值比较， 左子树的右值和右子树的左值比较，得到结果。

###### 迭代

迭代的思路跟递归有点像的，把比较的值放进栈里，取出来比较后再将子节点按规律压到栈里。比较完得到结果。

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
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        return recursive(root->left, root->right) && iter(root->left, root->right);
    }
    
    bool recursive(TreeNode* left, TreeNode* right) {
        if(!left && !right) return true;
        if(!left || !right) return false;
        return left->val == right->val && recursive(left->left, right->right) && recursive(left->right, right->left);
    }
    
    bool iter(TreeNode* left, TreeNode* right) {
        TreeNode* l,* r;
        stack<TreeNode*> s;
        s.push(left);
        s.push(right);
        while(!s.empty()) {
            l = s.top();
            s.pop();
            r = s.top();
            s.pop();
            if (!l && !r) continue;
            if (!l || !r) return false;
            if (l->val == r->val){
                s.push(l->left);s.push(r->right);
                s.push(l->right);s.push(r->left);
            } else {
                return false;
            }
            
        }
        return true;
    }
};
```

