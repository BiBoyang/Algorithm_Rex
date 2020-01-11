# LeetCode_0094 二叉树的中序遍历


## 解答
中序遍历，左->中->右。
### 递归法
```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        dfs(ans,root);        
        return ans;
    }
    void dfs(vector<int>& ans,TreeNode* root) {
        if(root==NULL) return;
        dfs(ans,root->left);
        ans.push_back(root->val);
        dfs(ans,root->right);   
    }
};
```
时间复杂度：O(n)。递归函数 T(n)=2⋅T(n/2)+1。   
空间复杂度：最坏情况下需要空间O(n)，平均情况为O(log⁡n)。

### 迭代
使用栈来迭代。

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;            
        stack<TreeNode*> nodeStack;
        while(root || !nodeStack.empty()) {
            while(root) {
                //不断的向左把节点压入栈里
                nodeStack.push(root);
                root = root->left;
            }
            root = nodeStack.top();
            ans.push_back(root->val);
            nodeStack.pop();
            root = root->right;
        }
        return ans;
    }
};
```
时间复杂度：O(n)。递归函数 T(n)=2⋅T(n/2)+1。   
空间复杂度：最坏情况下需要空间O(n)，平均情况为O(log⁡n)。