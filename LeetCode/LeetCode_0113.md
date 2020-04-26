# LeetCode_0113 路径总和II
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

# 解答
使用递归。
```C++
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> res;
        vector<int> temp;
        dfs(root, sum, res, temp);
        return res;
    }
    void dfs(TreeNode *root,int sum,vector<vector<int>>& total,vector<int> thisTotal) {
        if(root == NULL) return ;
        sum = sum - root->val;
        thisTotal.push_back(root->val);
        if(!root->left &&!root->right&&sum==0){
            total.push_back(thisTotal);
        }
        dfs(root->left, sum, total, thisTotal);
        dfs(root->right, sum, total, thisTotal);
    }
};
```