# 面试题28. 对称的二叉树

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```

示例 1：
```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

示例 2：
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

# 解答

## 递归法
```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return dfs(root,root);
    }
    bool dfs(TreeNode *A,TreeNode *B) {
        if(A == NULL || B == NULL) return true;
        if(A == NULL && B == NULL) return false;
        return (A->val == B->val) && dfs(A->left,B->right) && dfs(A->right,B->left);
    }
};
```

* 时间复杂度：O(n)。
* 空间复杂度：O(n)。最差树是一枝，O(n)。

## 迭代法
使用栈
```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        stack<TreeNode *>leftStack,rightStack;
        TreeNode *l = root->left;
        TreeNode *r = root->right;
        while(l || r || leftStack.size() || rightStack.size()) {
            while(l && r) {
                leftStack.push(l);
                l = l->left;
                rightStack.push(r);
                r = r->right;
            }
            if(l || r) return false;
            l = leftStack.top(),leftStack.pop();
            r = rightStack.top(),rightStack.pop();
            if(l->val != r->val) return false;
            l = l->right,r = r->left;
        }
         return true;
    }
};
```