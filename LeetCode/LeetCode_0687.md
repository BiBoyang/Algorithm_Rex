# LeetCode_0687 最长同值路径
给定一个二叉树，找到最长的路径，这个路径中的每个节点具有相同值。 这条路径可以经过也可以不经过根节点。

注意：两个节点之间的路径长度由它们之间的边数表示。

示例 1:

输入:
```
              5
             / \
            4   5
           / \   \
          1   1   5
```
输出:
```
2
```
示例 2:

输入:
```
              1
             / \
            4   5
           / \   \
          4   4   5
```          
输出:
```
2
```
注意: 给定的二叉树不超过10000个结点。 树的高度不超过1000。

# 解答

```C++
class Solution {
public:
    int help(TreeNode* node, int &ans) {
    if (node == nullptr) return 0;
    int left = help(node->left, ans);
    int right = help(node->right, ans);
    left = (node->left != nullptr && node->val == node->left->val) ? left + 1 : 0;
    right = (node->right != nullptr && node->val == node->right->val) ? right + 1 : 0;

    ans = max(ans, left + right);
    return max(left, right);
}

int longestUnivaluePath(TreeNode* root) {
    int ans = 0;
    help(root, ans);
    return ans;
}

};
```