
# LeetCode_0111 二叉树的最小深度
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例:

给定二叉树 [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```

# 解答
递归法。
也是同样的递归求值。
```C++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
        if((root->left == NULL) && (root->right == NULL)) {
            return 1;
        }
        int temp = INT_MAX;
        if(root->left != NULL) {
            temp = min(minDepth(root->left),temp);
        }
        if(root->right != NULL) {
            temp = min(minDepth(root->right),temp);
        }
        return temp+1;
    }
};
```
时间复杂度：O(n)。
空间复杂度：O(n)。

迭代法。
深度优先搜索。
```C++
class Solution {
public:
    int minDepth(TreeNode* root) {
        stack<pair<TreeNode*, int>> NodeStack;
        if(root == NULL) {
            return 0;
        } else {
            NodeStack.push(pair<TreeNode *,int>(root,1));
        }
        int min_depth = INT_MAX;
        while(!NodeStack.empty()) {
            pair<TreeNode*, int> current = NodeStack.top();
            NodeStack.pop();
            root = current.first;
            int current_depth = current.second;
            if((root->left == NULL) && (root->right == NULL)) {
                min_depth = min(min_depth,current_depth);
            }
            if(root->left != NULL) {
                NodeStack.push(pair<TreeNode*,int>(root->left,current_depth + 1));
            }
            if(root->right != NULL) {
                NodeStack.push(pair<TreeNode*,int>(root->right,current_depth + 1));
            }
        }
        return min_depth;
    }
};
```
时间复杂度：O(n)。
空间复杂度：O(n)。


