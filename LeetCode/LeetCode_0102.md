
# LeetCode_0102 二叉树的层次遍历

# 解答
## 递归法

```C++

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        helper(res,root,0);
        return res;
    }
    void helper(vector<vector<int>>& res,TreeNode* node,int level){
        if(node==NULL) return ;
        if(level >= res.size()){
            vector<int> level_res;
            res.push_back(level_res);
        }  
        res[level].push_back(node->val);
        if(node->left) helper(res,node->left,level+1);
        if(node->right) helper(res,node->right,level+1);
    }
};

```


## 迭代法
使用队列来暂时保存。
第 0 层只包含根节点 root ，算法实现如下：
* 初始化队列只包含一个节点 root 和层次编号 0 ： level = 0。
* 当队列非空的时候：
    * 在输出结果 levels 中插入一个空列表，开始当前层的算法。
    * 计算当前层有多少个元素：等于队列的长度。
    * 将这些元素从队列中弹出，并加入 levels 当前层的空列表中。
    * 将他们的孩子节点作为下一层压入队列中。
    * 进入下一层 level++。


```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
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
        return ans;
    }
};
```

