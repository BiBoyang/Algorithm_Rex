
# LeetCode_0145 二叉树的后序遍历
二叉树的后序遍历

# 解答
## 递归法
```C++
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root,res);
        return res;
    }
    void helper(TreeNode *node,vector<int> &res) {
        if(node == NULL) {
            return;
        }
        helper(node->left,res);
        helper(node->right,res);
        res.push_back(node->val);


    }

};
```


## 迭代法




