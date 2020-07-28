# LeetCode_0298 二叉树最长连续序列

给你一棵指定的二叉树，请你计算它最长连续序列路径的长度。

该路径，可以是从某个初始结点到树中任意结点，通过「父 - 子」关系连接而产生的任意路径。

这个最长连续的路径，必须从父结点到子结点，反过来是不可以的。

示例 1：
```
输入:

   1
    \
     3
    / \
   2   4
        \
         5

输出: 3

解析: 当中，最长连续序列是 3-4-5，所以返回结果为 3
```

示例 2：
```
输入:

   2
    \
     3
    / 
   2    
  / 
 1

输出: 2 

解析: 当中，最长连续序列是 2-3。注意，不是 3-2-1，所以返回 2。
```

# 解答
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
    int MaxLength = 0;
    void dfs(TreeNode *root,TreeNode *pre,int length) {
        if(root == NULL) return ;
        if(pre != NULL && root->val == pre->val + 1) {
            length = length + 1;
        } else {
            length = 1;
        }
        MaxLength = max(MaxLength,length);
        if(root->left) dfs(root->left,root,length);
        if(root->right) dfs(root->right,root,length);
    }
    
    int longestConsecutive(TreeNode* root) {
        if(root == NULL) return 0;
        dfs(root,NULL,0);
        return MaxLength;
    }
};
```
* 时间复杂度：O(N)。N 是二叉树节点个数
* 空间复杂度：O(N)。


