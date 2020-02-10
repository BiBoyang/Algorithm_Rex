
# LeetCode_0105 从前序与中序遍历序列构造二叉树
根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

# 解答
使用DFS来递归处理。
先序遍历的顺序是 Root -> Left -> Right，这就能方便的从根开始构造一棵树。

首先，preorder 中的第一个元素一定是树的根，这个根又将 inorder 序列分成了左右两棵子树。现在我们只需要将先序遍历的数组中删除根元素，然后重复上面的过程处理左右两棵子树。

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return dfs(0, preorder.size()-1, 0, inorder.size()-1, preorder, inorder);
    }

    TreeNode* dfs(int left_pre, int right_pre, int left_in, int right_in, vector<int>& preorder, vector<int>& inorder ){
        if(left_pre > right_pre || left_in > right_in){
            return NULL;
        }
        int rootin = left_in;
        while(rootin <= right_in && inorder[rootin] != preorder[left_pre]){
            ++ rootin;
        }
        TreeNode * ptrTreeNode = new TreeNode(preorder[left_pre]);
        int left_len = rootin - left_in;
        ptrTreeNode->left = dfs(left_pre + 1, right_pre, left_in, rootin - 1, preorder, inorder);
        ptrTreeNode->right = dfs(left_pre + left_len + 1, right_pre, rootin + 1, right_in, preorder, inorder);
        return ptrTreeNode;
    }
};
```

时间复杂度：O(N)，
空间复杂度：O(N)，存储整棵树的开销。

优化的方法：
我们可以使用hashTable来存储各数在中序中的位置，然后继续处理。
```C++
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {        
        unordered_map<int, int> Map;  //记录各数在中序中的位置
        for(int i = 0;i< inorder.size();i++) {
            Map[inorder[i]] = i;
        }
        return dfs(preorder, 0, preorder.size(), inorder, 0, inorder.size(), Map);
    }
    TreeNode* dfs(vector<int>& preorder, int preLeft, int preRight, vector<int>& inorder, int inLeft, int inRight,unordered_map<int, int>& Map) {
        if (preLeft >= preRight || inLeft >= inRight) return NULL;
        int pos = Map[preorder[preLeft]] - inLeft;  // 从中序序列获取左子树的长度
        auto root = new TreeNode(preorder[preLeft]);
        root->left = dfs(preorder, preLeft + 1, preLeft + pos + 1, inorder, inLeft, inLeft + pos + 1, Map);
        root->right = dfs(preorder, inLeft + pos + 1, inRight, inorder, preLeft + pos + 1, preRight, Map);
        return root;
    }
};

```