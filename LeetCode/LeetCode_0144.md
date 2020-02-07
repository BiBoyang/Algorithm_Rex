
# LeetCode_0094 二叉树的前序遍历

二叉树的前序遍历

# 解答
两种方法，递归和迭代。

## 递归

```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(res,root);
        return res;
    }
    void helper(vector<int> & res,TreeNode *node) {
        if(node == NULL) return;
        res.push_back(node->val);
        helper(res,node->left);
        helper(res,node->right);
    }
};
```
时间复杂度：O(n)。    
空闲复杂度：O(n)。

## 迭代
使用一个栈来保持需要的值。
从根节点开始，每次迭代弹出当前栈顶元素，并将其子节点压入栈中，先压左孩子再压右孩子。
```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode *>nodeStack;
        while(root || !nodeStack.empty()) {
            while(root) {
                nodeStack.push(root);
                res.push_back(root->val);
                root = root->left;
            }
            root = nodeStack.top();
            root = root->right;
            nodeStack.pop();
        }
        return res;   
    }
};
```
时间复杂度：O(n)。    
空闲复杂度：O(n)。
