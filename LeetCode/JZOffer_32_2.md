# 面试题32 - II. 从上到下打印二叉树 II

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其层次遍历结果：
```
[
  [3],
  [9,20],
  [15,7]
]
```

# 解答
```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        bfs(res,root,0);
        return res;
    }
    void bfs(vector<vector<int>> &res,TreeNode *node,int level) {
        if(node == NULL) return ;
        if(level == res.size()) {
            vector<int> level_res;
            res.push_back(level_res);
        }
        res[level].push_back(node->val);
        if(node->left) bfs(res,node->left,level+1);
        if(node->right) bfs(res,node->right,level+1);
    }
};
```
