
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

## 迭代法
我们知道，但凡使用递归解决的问题，都可以考虑一下栈。
所以我们从包含根结点且相应深度为 1 的栈开始。然后我们继续迭代：将当前结点弹出栈并推入子结点。每一步都会更新深度。
```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        stack<pair<TreeNode*,int>> NodeStack;
        int maxdeep = 0,deep = 0;
        //若栈非空，则说明还有一些节点的右子树尚未探索；若p非空，意味着还有一些节点的左子树尚未探索
        while(root || !NodeStack.empty()) {
            //优先往左边走
            while(root) {
                //记录深度
                deep++;
                NodeStack.push(pair<TreeNode*,int>(root,deep));
                root = root->left;
            }
            //若左边无路，就预备右拐。右拐之前，记录右拐点的基本信息
            root = NodeStack.top().first;
            deep = NodeStack.top().second;
            //比较当前节点深度和之前存储的最大深度
            maxdeep = max(maxdeep,deep);
            root = root->right;
            //将右拐点出栈；此时栈顶为右拐点的前一个结点。在右拐点的右子树全被遍历完后，会预备在这个节点右拐
            NodeStack.pop();
        }
        return maxdeep;
    }
};
```