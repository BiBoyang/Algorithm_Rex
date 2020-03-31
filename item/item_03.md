# 二叉树的刷题之旅（二）：深度问题
| name  | link  | info  |
|---|---|---|
|[104. 二叉树的最大深度](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)     | [C++](https://github.com/BiBoyang/Algorithm_Rex/blob/master/LeetCode/LeetCode_0144.md)  |   |
|[111. 二叉树的最小深度](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)     | [C++](https://github.com/BiBoyang/Algorithm_Rex/blob/master/LeetCode/LeetCode_0144.md)  |   |
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
时间复杂度：O(n)。
空间复杂度：O(n)。
我们知道，但凡使用递归解决的问题，都可以考虑一下`栈`。
所以我们从包含根结点且相应深度为 1 的栈开始。然后我们继续迭代：将当前结点弹出栈并推入子结点。每一步都会更新深度。

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        int ans = 0;
        if(root == NULL) return ans;
        //这个栈用来记录节点和深度
        stack<pair<TreeNode*,int>> nodeStack;
        int deep = 0;
        while(root || !nodeStack.empty()) {
            while(root) {
                deep++;
                nodeStack.push(pair<TreeNode*,int>(root,deep));
                root = root->left;
            }
            root = nodeStack.top().first;
            deep = nodeStack.top().second;
            ans = max(ans, deep);
            nodeStack.pop();
            root = root->right;
        }
        return ans;
    }
};

```
时间复杂度：O(n)。
空间复杂度：O(n)。


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
时间复杂度：O(n)。
空间复杂度：O(n)。

迭代法。
深度优先搜索。
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
时间复杂度：O(n)。
空间复杂度：O(n)。


## N叉树的最大深度
直接递归。
```C++
class Solution {
public:
    int maxDepth(Node* root) {
        int ans = 0;
        if(root == NULL) {
            return 0;
        } else {
            for(auto child:root->children) {
                if(child) {
                    ans = max(ans,maxDepth(child));
                }
            }
        }
        return ans + 1;
    }
};
```

