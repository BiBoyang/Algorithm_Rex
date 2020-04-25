# 面试题32 - III. 从上到下打印二叉树 III
请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：
```
[
  [3],
  [20,9],
  [15,7]
]
```

# 解答


奇偶层的打印顺序不一样是相反的，可以利用层数偶数与否调用reverse来解决，但是海量数据时这个效率很低，不推荐。

因为奇数层的打印顺序是从左到右，偶数层的打印顺序是从右到左，可以利用STL容器deque中
push_back(),push_front(),front(),back(),pop(),popfront()来实现



```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (root==NULL) return res;
        
        bool flag = true; //从左向右打印为true，从右向左打印为false
        deque<TreeNode*> q;
        q.push_back(root);
        while (!q.empty()) {
            int n = q.size();
            vector<int> out;
            TreeNode* node;
            while (n>0) {
                // 前取后放：从左向右打印，所以从前边取，后边放入
                if (flag) {
                    node = q.front();
                    q.pop_front();
                    if (node->left) q.push_back(node->left);  // 下一层顺序存放至尾
                    if (node->right) q.push_back(node->right);
                } else {
                    //后取前放： 从右向左，从后边取，前边放入
                    node = q.back();
                    q.pop_back();
                    if (node->right) q.push_front(node->right);  // 下一层逆序存放至首
                    if (node->left) q.push_front(node->left);
                }
                out.push_back(node->val);
                n--;
            }
            flag = !flag;
            res.push_back(out);
        }
        return res;
    }
};

```