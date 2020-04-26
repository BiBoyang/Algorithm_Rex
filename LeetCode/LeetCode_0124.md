# LeetCode_0124 二叉树中的最大路径和

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1:
```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6
```
示例 2:
```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```

# 解答

二叉树 abc，a 是根结点（递归中的 root），bc 是左右子结点（代表其递归后的最优解）。
最大的路径，可能的路径情况：
```
    a
   / \
  b   c
```
1. b + a + c。
2. b + a + a 的父结点。
3. a + c + a 的父结点。

其中情况 1，表示如果不联络父结点的情况，或本身是根结点的情况。

这种情况是没法递归的，但是结果有可能是全局最大路径和。

情况 2 和 3，递归时计算 a+b 和 a+c，选择一个更优的方案返回，也就是上面说的递归后的最优解啦。

```C++
class Solution {
public:
    int maxPathSum(TreeNode* root) {
        int sum = INT_MIN;
        maxPath(root, sum);
        return sum;
    }
    int maxPath(TreeNode *root,int &sum) {
        if(root == NULL) return 0;
        //计算左边分支最大值
        int left = max(maxPath(root->left, sum),0);
        //计算右边分支最大值
        int right = max(maxPath(root->right,sum), 0);
        //计算 左->根->右 路线上的最大值
        int lmr = root->val + left +right;
        // 左->根->右 和 历史最大值做对比
        sum = max(sum, lmr);
        // 返回经过root的单边最大分支给上游
        return root->val + max(left,right);
    }
};
```
* 时间复杂度：O(N)其中 N 是结点个数。我们对每个节点访问不超过 2 次。
* 空间复杂度：O(log⁡(N))。我们需要一个大小与树的高度相等的栈开销，对于二叉树空间开销是 O(log⁡(N))。

