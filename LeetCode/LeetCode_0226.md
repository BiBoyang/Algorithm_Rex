
# LeetCode_0226 翻转二叉树

翻转一棵二叉树。

示例：
```
输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9

输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1

```

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
    TreeNode* invertTree(TreeNode* root) {
        if(root == NULL) return NULL;
        TreeNode *temp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(temp);
        return root;

    }
};
```

## 迭代法
使用队列。


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
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return NULL;
        queue<TreeNode *>nodeQueue;
        nodeQueue.push(root);
        while(!nodeQueue.empty()) {
            TreeNode *node = nodeQueue.front(); 
            nodeQueue.pop();
            TreeNode *tmp = node->left;
            node->left = node->right;
            node->right = tmp;
            if (node->left) nodeQueue.push(node->left);
            if (node->right) nodeQueue.push(node->right);



        }
        return root;

    }
};
```