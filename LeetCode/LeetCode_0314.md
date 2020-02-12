
# LeetCode_0314 二叉树的垂直遍历

给定一个二叉树，返回其结点 垂直方向（从上到下，逐列）遍历的值。

如果两个结点在同一行和列，那么顺序则为 从左到右。

示例 1：
```
输入: [3,9,20,null,null,15,7]

   3
  /\
 /  \
9   20
    /\
   /  \
  15   7 

输出:

[
  [9],
  [3,15],
  [20],
  [7]
]
```
示例 2:
```
输入: [3,9,8,4,0,1,7]

     3
    /\
   /  \
  9    8
  /\   /\
 /  \ /  \
4   0 1   7 

输出:

[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```
示例 3:
```
输入: [3,9,8,4,0,1,7,null,null,null,2,5]（注意：0 的右侧子节点为 2，1 的左侧子节点为 5）

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

输出:

[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

# 解答

应该使用层序遍历，保证深度较小的节点最先被遍历。
注意应该使用map容器，unordered_map虽然查询是O(1)时间复杂度，但是不具备顺序属性。

```C++
class Solution {
public:
    vector<vector<int>> verticalOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if(root == NULL) return ans;
        map<int,int> hasht;
        queue<TreeNode*> q;
        queue<int> state;


        q.push(root);
        state.push(0);

        while(q.size()!=0){
            auto temp = q.front();
            auto temp_state = state.front();
            q.pop();
            state.pop();

            if(hasht.find(temp_state) == hasht.end()){
                vector<int> ans_layer;
                ans_layer.push_back(temp->val);
                ans.push_back(ans_layer);
                hasht[temp_state] = ans.size()-1;
            }
            else{
                ans[hasht[temp_state]].push_back(temp->val);
            }
            if(temp->left != NULL){
                q.push(temp->left);
                state.push(temp_state - 1);
            }
            if(temp->right != NULL){
                q.push(temp->right);
                state.push(temp_state + 1);
            }           
        }
        vector<vector<int>> ordered_ans;
        for(auto &it:hasht){
            ordered_ans.push_back(ans[(it).second]);
        }
        return ordered_ans;
    }
};

```

优化一下
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
    vector<vector<int>> verticalOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if (root == NULL) return ans;
        map<int, vector<int>> m;
        queue<pair<TreeNode*, int>> q;
        q.push(make_pair(root, 0));
        while(!q.empty()) {
            pair<TreeNode*, int> t1 = q.front();
            q.pop();
            m[t1.second].push_back(t1.first->val);
            if (t1.first->left) {
                q.push(make_pair(t1.first->left, t1.second - 1));
            }
            if (t1.first->right) {
                q.push(make_pair(t1.first->right, t1.second + 1));
            }
        }


        for (auto it : m) {
            ans.push_back(it.second);
        }
        return ans;
    }
};

```