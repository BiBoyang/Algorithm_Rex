# LeetCode_0549. 二叉树中最长的连续序列
给定一个二叉树，你需要找出二叉树中最长的连续序列路径的长度。

请注意，该路径可以是递增的或者是递减。例如，[1,2,3,4] 和 [4,3,2,1] 都被认为是合法的，而路径 [1,2,4,3] 则不合法。另一方面，路径可以是 子-父-子 顺序，并不一定是 父-子 顺序。

示例 1:
```
输入:
        1
       / \
      2   3
输出: 2
解释: 最长的连续路径是 [1, 2] 或者 [2, 1]。
 ```

示例 2:
```
输入:
        2
       / \
      1   3
输出: 3
解释: 最长的连续路径是 [1, 2, 3] 或者 [3, 2, 1]。
``` 

注意: 树上所有节点的值都在 [-1e7, 1e7] 范围内。


# 解答
```C++
class Solution {
public:
    int res = 0;
    //pair 第一位表示递减。第二位表示递增
    pair<int, int> dfs(TreeNode* root) {
        if (root == NULL) return {0, 0};
        auto l = dfs(root->left);
        auto r = dfs(root->right);
        int l1 = 0;
        int l2 = 0;
        int r1 = 0;
        int r2 = 0;
        if (root->right && root->right->val + 1 == root->val) {
            r1 = r.first;
        } else if (root->right && root->right->val - 1 == root->val) {
            r2 = r.second;
        }
        if (root->left && root->left->val + 1 == root->val) {
            l1 = l.first;
        } else if (root->left && root->left->val - 1 == root->val) {
            l2 = l.second;
        }
        int len = max(l1 + 1 + r2, l2 + 1 + r1);
        res = max(res, len);
        return {max(l1, r1) + 1, max(l2, r2) + 1};
    }
    int longestConsecutive(TreeNode* root) {
        dfs(root);
        return res;
    }
};
```