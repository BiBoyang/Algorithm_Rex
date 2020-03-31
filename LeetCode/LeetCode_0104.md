
# LeetCode_0104 二叉树的最大深度

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。

# 解答

## 递归法
```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == NULL) {
            return 0;
        } else {
            int left_height =  maxDepth(root->left);
            int right_height = maxDepth(root->right);
            return max(left_height,right_height) + 1;
        }
    }
};

```
时间复杂度：O(n)。
空间复杂度：O(n)。

## 迭代法
我们知道，但凡使用递归解决的问题，都可以考虑一下栈。
所以我们从包含根结点且相应深度为 1 的栈开始。然后我们继续迭代：将当前结点弹出栈并推入子结点。每一步都会更新深度。
```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int ans = 0;
        if(root == NULL) return ans;
        //这个栈用来记录节点和深度
        stack<pair<TreeNode*,int>> nodeStack;
        int deep = 0;
        while(root || !nodeStack.empty()) {
            while(root) {
                deep++;
                nodeStack.push(pair<TreeNode*,int>(root,deep));
                root = root->left;
            }
            root = nodeStack.top().first;
            deep = nodeStack.top().second;
            ans = max(ans, deep);
            nodeStack.pop();
            root = root->right;
        }
        return ans;
    }
};
```
时间复杂度：O(n)。
空间复杂度：O(n)。