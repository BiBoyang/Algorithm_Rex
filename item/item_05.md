# 二叉树的刷题之旅（三）：路径问题

问题汇总

1. 路径总和   
2. 路径总和 II   
3. 二叉树中的最大路径和   
4. 求根到叶子节点数字之和   
5. 二叉树的所有路径   
6. 路径总和 III   
7. 二叉树的直径   
8. 二叉树中最长的连续序列   
9. 路径和 IV   
10. 最长同值路径   

# LeetCode_112 路径总和
给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

示例: 
给定如下二叉树，以及目标和 sum = 22，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。


# 解答

## 递归法
最直接的方法就是利用递归，遍历整棵树：如果当前节点不是叶子，对它的所有孩子节点，递归调用 hasPathSum 函数，其中 sum 值减去当前节点的权值；如果当前节点是叶子，检查 sum 值是否为 0，也就是是否找到了给定的目标和。

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if(root == NULL) return false;
        sum = sum - root->val;
        if((root->left == NULL) && (root->right == NULL)) {
            if(sum == 0) {
                return true;
            } else {
                return false;
            }
        }
        return hasPathSum(root->left, sum) || hasPathSum(root->right, sum);
    }
};
```
* 时间复杂度: O(n), 需要访问每一个结点，所以时间复杂度为O(n)
* 空间复杂度: 最好情况，当树是完全二叉树时，递归的深度为log(n), 所以最多需要log(n)的函数调用栈空间；最坏情况，当树退化为链表时，递归的深度为n, 需要n的函数调用中空间。


## 迭代法
使用栈
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
    bool hasPathSum(TreeNode* root, int sum) {
        if(root == NULL) return false;
        stack<pair<TreeNode *, int>> nodeStack;
        nodeStack.push(make_pair(root,sum));
        while(!nodeStack.empty()) {
            TreeNode *node = nodeStack.top().first;
            sum = nodeStack.top().second;
            nodeStack.pop();
            if(node->left == NULL && node->right == NULL && node->val == sum) {
                return true;
            }
            if(node->left) {
                nodeStack.push(make_pair(node->left,sum - node->val));
            }
            if(node->right) {
                nodeStack.push(make_pair(node->right, sum - node->val));
            }
        }
        return false;
    }
};
```

* 时间复杂度: O(n), 需要访问每一个结点，所以时间复杂度为O(n)
* 空间复杂度:当树不平衡的最坏情况下是 O(N) 。在最好情况（树是平衡的）下是 O(log⁡N)。