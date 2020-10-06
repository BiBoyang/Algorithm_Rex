# LeetCode_652 寻找重复的子树
给定一棵二叉树，返回所有重复的子树。对于同一类的重复子树，你只需要返回其中任意一棵的根结点即可。

两棵树重复是指它们具有相同的结构以及相同的结点值。

示例 1：
```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```
下面是两个重复的子树：
```
      2
     /
    4
```
和
```
    4
```
因此，你需要以列表的形式返回上述重复子树的根结点。

#  解答
使用层序遍历

```
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
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        vector<TreeNode*> result;
        unordered_map<string,int> hashMap;
        helper(root,result,hashMap);
        return result;
    }
    string helper(TreeNode*root,vector<TreeNode*>&result,
                  unordered_map<string,int>&hashMap) {
        //使用层序遍历
        string str;
        if(!root) return "#";
        str = to_string(root->val) + ' ' + helper(root->left,result,hashMap) + ' '+helper(root->right,result,hashMap);
        if(hashMap[str] == 1) result.push_back(root);
        hashMap[str]++;
        return str;
    }
};
``` 