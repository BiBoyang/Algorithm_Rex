
# LeetCode_0107 二叉树的层次遍历 II
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其自底向上的层次遍历为：
```
[
  [15,7],
  [9,20],
  [3]
]
```
# 解答
## 递归法
和正方向层次遍历一样的方法，只不过最后进行调换、

```C++
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res;
        levelorder(root,0,res);
        return vector<vector<int>>(res.rbegin(),res.rend());
    }
        
    void levelorder(TreeNode* node, int level, vector<vector<int>>& res) 
    {
        if(!node) return ;
        if(res.size()==level) res.push_back({});
        res[level].push_back(node->val);
        if(node->left) levelorder(node->left,level+1, res);
        if(node->right) levelorder(node->right,level+1,res);
    }
    
};
```
或者
```C++
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> ans;
        dfs(root,0,ans);
        reverse(ans.begin(),ans.end());
        return ans;
    }
    
    void dfs(TreeNode* root,int level,vector<vector<int>>& ans){
        if(!root) return;
        if(level >= ans.size()) ans.push_back(vector<int>());
        ans[level].push_back(root->val);
        dfs(root->left,level+1,ans);
        dfs(root->right,level+1,ans);
    }   
};

```

时间复杂度：O(N)，因为每个节点恰好会被运算一次。
空间复杂度：O(N)，保存输出结果的数组包含 N 个节点的值。

## 迭代法

```C++
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> nodeQueue;
        if(root) {
            nodeQueue.push(root);
        }

        while(nodeQueue.size()){
            //加入空vector
            ans.push_back(vector<int>());
            int cnt = nodeQueue.size();
            for(int i = 0;i<cnt;++i){
                TreeNode* cur = nodeQueue.front();
                nodeQueue.pop();
                int t = ans.size() - 1;
                ans[t].push_back(cur->val);
                if(cur->left) {
                    nodeQueue.push(cur->left);
                }
                if(cur->right) {
                    nodeQueue.push(cur->right);
                }
            }
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};

```