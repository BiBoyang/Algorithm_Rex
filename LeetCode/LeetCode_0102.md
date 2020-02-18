
# LeetCode_0102 二叉树的层次遍历
给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。
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
## 递归法
最简单的解法就是递归，首先确认树非空，然后调用递归函数 bfs(node, level)，参数是当前节点和节点的层次。程序过程如下：

* 输出列表称为 levels，当前最高层数就是列表的长度 len(levels)。比较访问节点所在的层次 level 和当前最高层次 len(levels) 的大小，如果前者更大就向 levels 添加一个空列表。
* 将当前节点插入到对应层的列表 levels[level] 中。
* 递归非空的孩子节点：bfs(node.left / node.right, level + 1)。


```C++
class Solution {
public·:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        bfs(res,root,0);
        return res;
    }
    void bfs(vector<vector<int>>& res,TreeNode* node,int level){
        if(node==NULL) return ;
        if(level >= res.size()){
            vector<int> level_res;
            res.push_back(level_res);
        }  
        res[level].push_back(node->val);
        if(node->left) bfs(res,node->left,level+1);
        if(node->right) bfs(res,node->right,level+1);
    }
};
```
时间复杂度：O(N)，因为每个节点恰好会被运算一次。
空间复杂度：O(N)，保存输出结果的数组包含 N 个节点的值。

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

