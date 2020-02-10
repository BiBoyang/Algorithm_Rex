
# LeetCode_0095  不同的二叉搜索树 II
给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。

# 解答
使用DFS
```C++
class Solution {
public:
    vector<TreeNode*> helper(int start,int end){
        vector<TreeNode*> res;
        if(start > end) {
            res.push_back(nullptr);
        }
        for(int i=start;i<=end;i++) {
            vector<TreeNode*> leftVec = helper(start,i-1);
            vector<TreeNode*> rightVec = helper(i+1,end);
            //构建二叉树
            for(auto leftNode : leftVec) {
                for(auto rightNode : rightVec) {
                    TreeNode* root = new TreeNode(i);
                    root->left = leftNode;
                    root->right = rightNode;
                    res.push_back(root);
                }
            }
        }
        return res;
    }
    vector<TreeNode*> generateTrees(int n) {
        vector<TreeNode*> res;
        if(n == 0) {
            return res;    
        }
        res = helper(1,n);
        return res;
    }
};
```