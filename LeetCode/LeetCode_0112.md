# 112. 路径总和

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
·

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
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if (root == nullptr) return false;
        
        stack<pair<TreeNode *, int>> __stack;
        __stack.push(make_pair(root, sum));

        while (!__stack.empty()) {
            auto &item = __stack.top();
            auto node = item.first;
            sum = item.second;
            __stack.pop();

            if (node->left == nullptr && node->right == nullptr && node->val == sum) {
                return true;
            }

            if (node->left) {
                __stack.push(make_pair(node->left, sum - node->val));
            }

            if (node->right) {
                __stack.push(make_pair(node->right, sum - node->val));
            }
        }

        return false;
    }
};

作者：nchkdxlq
链接：https://leetcode-cn.com/problems/path-sum/solution/di-gui-jie-fa-die-dai-jie-fa-by-nchkdxlq/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```