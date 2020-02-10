
# LeetCode_0101 对称二叉树
给定一个二叉树，检查它是否是镜像对称的。

# 解答

## 迭代法

队列中每两个连续的结点应该是相等的，而且它们的子树互为镜像。最初，队列中包含的是 root 以及 root。该算法的工作原理类似于 BFS，但存在一些关键差异。每次提取两个结点并比较它们的值。然后，将两个结点的左右子结点按相反的顺序插入队列中。当队列为空时，或者我们检测到树不对称（即从队列中取出两个不相等的连续结点）时，该算法结束。

```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        queue<TreeNode*> q1, q2;
        q1.push(root->left);
        q2.push(root->right);
                
        while (!q1.empty() && !q2.empty()) {
            //把左右node分别构建新的树
            TreeNode *node1 = q1.front();
            TreeNode *node2 = q2.front();
            //记得一定要把q1、q2的元素出队列，不然会炸
            q1.pop();
            q2.pop();

            //如果两个树里有一个树没了，就说明不是对称的
            if((node1 && !node2) || (!node1 && node2)) {
                return false;
            }   
            if (node1 && node2) {
                //如果左元素和右元素不相等，则表示不对称
                if (node1->val != node2->val) {
                    return false;
                }
                //q1是左子树的队列，把元素从左往右加
                q1.push(node1->left);
                q1.push(node1->right);
                //q2是右子树的队列，把元素从右往左加
                q2.push(node2->right);
                q2.push(node2->left);
            }
        }
        return true;
    }
};
```



此外，这里还可以使用栈来处理，原理类似。
```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        stack<TreeNode *>left,right;
        auto l = root->left,r = root->right;
        while(l || r || left.size() || right.size()) {
            while(l && r) {
                left.push(l),l = l->left;
                right.push(r),r = r->right;
            }
            if(l || r) return false;
            l = left.top(),left.pop();
            r = right.top(),right.pop();
            if(l->val != r->val) return false;
            l = l->right,r = r->left;
        }
         return true;
    }
};
```
时间复杂度：O(n)，因为我们遍历整个输入树一次，所以总的运行时间为 O(n)，其中 n 是树中结点的总数。
空间复杂度：搜索队列需要额外的空间。在最糟糕情况下，我们不得不向队列中插入 O(n) 个结点。因此，空间复杂度为 O(n)。




## 递归法


```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return isMirror(root,root);
    }
    bool isMirror(TreeNode *node1,TreeNode *node2) {
        // if(node1 == NULL && node2 == NULL) return true;
        // if(node1 == NULL || node2 == NULL) return false;
        if(!node1 || !node2) return !node1 && !node2;
        return (node1->val == node2->val) && isMirror(node1->left,node2->right) && isMirror(node1->right,node2->left); 
    }
};
```

时间复杂度：O(n)，因为我们遍历整个输入树一次，所以总的运行时间为 O(n)，其中 n 是树中结点的总数。
空间复杂度：递归调用的次数受树的高度限制。在最糟糕情况下，树是线性的，其高度为 O(n)。因此，在最糟糕的情况下，由栈上的递归调用造成的空间复杂度为 O(n)。

