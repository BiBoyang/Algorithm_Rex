# 面试题26. 树的子结构
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:
```
     3
    / \
   4   5
  / \
 1   2
 ```
给定的树 B：
```
   4 
  /
 1
```

返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：

```
输入：A = [1,2,3], B = [3,1]
输出：false
```

示例 2：

```C++
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```



## 解答

先序遍历A中的每个节点

然后dfs判断b是否是a的子结构（若当前值相同，就递归左边和右边是否相同）

```C++
class Solution {
public:
    bool dfs(TreeNode *A,TreeNode *B){
        if(A == NULL || B == NULL) {
            return B == NULL ? true:false;
        }
        if(A->val != B->val) {
            return false;
        }
        return dfs(A->left,B->left) && dfs(A->right,B->right);
    }
    
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if(A == NULL || B == NULL) {
            return false;
        }
        return dfs(A,B) || isSubStructure(A->left,B) || isSubStructure(A->right, B);
    }
};
```

时间复杂度：O（MN）。MN分别是A、B的节点数量

空间复杂度：O(M)。

