# LeetCode_0099 恢复二叉搜索树
二叉搜索树中的两个节点被错误地交换。

请在不改变其结构的情况下，恢复这棵树。

# 解答
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
    void recoverTree(TreeNode* root) {
        TreeNode* first = NULL;
        TreeNode* second = NULL;
        TreeNode* pre = NULL;
        TreeNode* current = root;
        TreeNode* tmp = NULL;
        while(current != NULL) {
            if(current->left == NULL) {     
                //左子树为空
                if((pre != NULL) && (pre->val > current->val)) {
                    //如果有前驱且前驱的值大于当前结点的值,说明顺序反了,存在错误结点
                    if(first == NULL) {  
                        //如果是第一次发现,则将first置为前驱,second置为当前结点
                        first = pre;
                        second = current;
                    } else {              
                        //如果不是第一次发现,说明存在两个不相邻位置的交换,将second改为后者
                        second = current;
                    }
                }
                pre = current;             
                //如果没有前驱或者前驱的值小于当前值,属于正常情况,则继续遍历
                current = current->right;
            } else {
                tmp = current->left;
                while((tmp->right != NULL) && (tmp->right != current)) {
                    tmp = tmp->right;
                }
                if(tmp->right == NULL) {
                    tmp->right = current;
                    current = current->left;
                } else {
                    tmp->right = NULL;//恢复树的形状
                    if((pre != NULL) && (pre->val > current->val)) {//判断逻辑与上面的相同
                        if(first == NULL) {
                            first = pre;
                            second = current;
                        } else {
                            second = current;
                        }
                    }
                    pre = current;
                    current = current->right;
                }
            }
        }
        int itmp = first->val;
        first->val = second->val;
        second->val = itmp;
    }
};
```