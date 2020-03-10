
# LeetCode_0543 二叉树的直径

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

示例 :
给定二叉树
```
          1
         / \
        2   3
       / \     
      4   5    
```
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

注意：两结点之间的路径长度是以它们之间边的数目表示。

# 解答
递归求解。
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
    int dfs(TreeNode *root,int& ans) {
        if(root == NULL) return 0;
        int LeftLen = dfs(root->left, ans);
        int RightLen = dfs(root->right, ans);
        
        ans  = max(ans, LeftLen+RightLen);
        return max(LeftLen, RightLen) + 1;
    }

    int diameterOfBinaryTree(TreeNode* root) {
        if(root==NULL)  return 0;
        int cnt=0;//保存最大直径
        dfs(root,cnt);
        return cnt;
    }
};
```