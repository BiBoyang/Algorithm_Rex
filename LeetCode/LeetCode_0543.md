
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
我们定义一个递归函数 dfs(node) 计算当前节点为根节点的最大深度，函数返回该节点为根的子树的深度。先递归调用左儿子和右儿子求得它们为根的子树的深度 LeftLen 和 RightLen ，则该节点为根的子树的深度即为 max(LeftLen, RightLen) + 1


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
    int ans = 0;
    int dfs(TreeNode *root) {
        if(root == NULL) return 0;
        int LeftLen = dfs(root->left);
        int RightLen = dfs(root->right);
        ans  = max(ans, LeftLen+RightLen); // 计算d_node即L+R+1 并更新ans
        return max(LeftLen, RightLen) + 1;// 返回该节点为根的子树的深度
    }

    int diameterOfBinaryTree(TreeNode* root) {
        if(root==NULL)  return 0;
        dfs(root);
        return ans;
    }
};
```