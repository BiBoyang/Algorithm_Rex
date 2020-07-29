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
    int helper(TreeNode* node, int &ans) {
        if (node == NULL) return 0;

        int leftLen = helper(node->left, ans);
        int rightLen = helper(node->right, ans);

        if(node->left && node->val == node->left->val) {
            leftLen =  leftLen + 1;
        } else {
            leftLen = 0;
        }

        if(node->right && node->val == node->right->val) {
            rightLen = rightLen + 1;
        } else {
            rightLen = 0;
        }

        ans = max(ans, leftLen + rightLen);
        return max(leftLen, rightLen);
    }
    int longestUnivaluePath(TreeNode* root) {
        int ans = 0;
        helper(root, ans);
        return ans;
    }
};
```