
# LeetCode_0145 二叉树的后序遍历
二叉树的后序遍历

# 解答
## 递归法
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root,res);
        return res;
    }
    void helper(TreeNode *node,vector<int> &res) {
        if(node == NULL) {
            return;
        }
        helper(node->left,res);
        helper(node->right,res);
        res.push_back(node->val);


    }

};
```


## 迭代法
迭代法。从根节点开始依次迭代，弹出栈顶元素输出到输出列表中，然后依次压入它的所有孩子节点，按照从上到下、从右至左的顺序依次压入栈中。
因为深度优先搜索后序遍历的顺序是从下到上、从左至右，所以需要将输出列表逆序输出。
这里有点绕，可能刚开始有点绕不过来。画个图。

```
                A
               / \
             /     \
            B        C
           / \      / \
          /   \    /   \
         D    E    F    G
``` 
      
|temp|NodeStack|res|
|---|---|---|
|A|AEB||        
|B|AEBDC|| 
|C|AEBDC|C| 
|D|AEBD|CD|          
|B|AEB|CDB| 
|E|AEGF|CDB| 
|F|AEGF|CDBF| 
|G|AEG|CDBFG| 
|E|AE|CDBFGE| 
|A|A|CDBFGEA| 

```C++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root==NULL) {
            return ans;
        }
        stack<TreeNode*> nodeStack;
        TreeNode *temp = root;
        nodeStack.push(temp);
        while(!nodeStack.empty()) {
            //这里每次循环的时候，都要把temp刷新。
            temp = nodeStack.top();
            if(!temp->left && !temp->right) {
                nodeStack.pop();
                ans.push_back(temp->val);
            }
            //一定要先添加右子
            if(temp->right) {
                nodeStack.push(temp->right);
                temp->right = NULL;
            }
            if(temp->left) {
                nodeStack.push(temp->left);
                temp->left = NULL;
            }    
        }
        return ans;
    }
};
```



