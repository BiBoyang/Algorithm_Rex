# LeetCode_0257 二叉树的所有路径
给定一个二叉树，返回所有从根节点到叶子节点的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
```C++
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

# 解答
万能的递归法，还是递归执行深度优先搜索


```C++
class Solution {
public:
    vector<string> res;
    vector<string> binaryTreePaths(TreeNode* root) {
        if(root == NULL) return res;
        string str = "";
        dfs(root, str);
        return res;
    }

    void dfs(TreeNode* root,string str) {
        if (root == NULL) return;  
        if (root->left == NULL && root->right == NULL) {
            str += to_string(root->val);
            res.push_back(str);
        }
        str = str + to_string(root->val) + "->";
        if(root->left) dfs(root->left, str);
        if(root->right) dfs(root->right, str);
    }
};
```