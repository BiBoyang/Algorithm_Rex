# 二叉树的刷题之旅（二）：对称、深度、子树、路径等问题
| name  | link  | info  |
|---|---|---|
|[104. 二叉树的最大深度](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)     | [C++](https://github.com/BiBoyang/Algorithm_Rex/blob/master/LeetCode/LeetCode_0144.md)  |   |
## 二叉树的最大深度
最简单的办法就是使用DFS的递归。
```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == NULL) {
            return 0;
        } else  {
            int left_depth = maxDepth(root->left);
            int right_depth = maxDepth(root->right);
            return max(left_depth,right_depth) + 1;
        }
    }
};
```
我们知道，但凡使用递归解决的问题，都可以考虑一下`栈`。
所以我们从包含根结点且相应深度为 1 的栈开始。然后我们继续迭代：将当前结点弹出栈并推入子结点。每一步都会更新深度。

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==NULL) return 0;
        stack<pair<TreeNode*,int>> s;
        TreeNode *p = root;
        int Maxdeep = 0;
        int deep = 0;
        
        //若栈非空，则说明还有一些节点的右子树尚未探索；若p非空，意味着还有一些节点的左子树尚未探索
        while(!s.empty() || p != NULL) {
            //优先往左边走
            while(p!=NULL) {
                //记录深度
                s.push(pair<TreeNode*,int>(p,++deep));
                p=p->left;
            }
            p = s.top().first;//若左边无路，就预备右拐。右拐之前，记录右拐点的基本信息
            deep=s.top().second;
            Maxdeep = max(Maxdeep,deep);//比较当前节点深度和之前存储的最大深度
            s.pop();//将右拐点出栈；此时栈顶为右拐点的前一个结点。在右拐点的右子树全被遍历完后，会预备在这个节点右拐
            p=p->right;
        }
        return Maxdeep;
    }
};
```

## 二叉树的最小深度
递归法。
也是同样的递归求值。
```C++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == NULL) {
            return 0;
        }
        if((root->left == NULL) && (root->right == NULL)) {
            return 1;
        }
        int temp = INT_MAX;
        if(root->left != NULL) {
            temp = min(minDepth(root->left),temp);
        }
        if(root->right != NULL) {
            temp = min(minDepth(root->right),temp);
        }
        return temp+1;
    }
};
```

迭代法。
```C++
class Solution {
public:
    int minDepth(TreeNode* root) {
        stack<pair<TreeNode*, int>> NodeStack;
        if(root == NULL) {
            return 0;
        } else {
            NodeStack.push(pair<TreeNode *,int>(root,1));
        }
        int min_depth = INT_MAX;
        while(!NodeStack.empty()) {
            pair<TreeNode*, int> current = NodeStack.top();
            NodeStack.pop();
            root = current.first;
            int current_depth = current.second;
            if((root->left == NULL) && (root->right == NULL)) {
                min_depth = min(min_depth,current_depth);
            }
            if(root->left != NULL) {
                NodeStack.push(pair<TreeNode*,int>(root->left,current_depth + 1));
            }
            if(root->right != NULL) {
                NodeStack.push(pair<TreeNode*,int>(root->right,current_depth + 1));
            }
        }
        return min_depth;
    }
};
```