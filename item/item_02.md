# 二叉树的各种遍历
##  树的概念
树里的每一个节点有一个根植和一个包含所有子节点的列表。从图的观点来看，树也可视为一个拥有N 个节点和N-1 条边的一个有向无环图。

二叉树是一种更为典型的树树状结构。如它名字所描述的那样，二叉树是每个节点最多有两个子树的树结构，通常子树被称作“左子树”和“右子树”。
树节点的声明在结构上类似于双链表的声明：在声明中，一个节点就是由   **Key(关键字)** 加上两个指向 **其他节点的指针(Left和Right)** 组成的结构。
遍历二叉树，我们有四种方式。
* 先序遍历 
  对节点的处理工作是在它的诸儿子节点被处理之前进行的；首先访问根节点，然后遍历左子树，最后遍历右子树。实际上是DFS。
  
* 后序遍历  
  对节点的处理工作是在它的诸儿子节点被计算后进行的；先遍历左子树，然后遍历右子树，最后访问树的根节点。实际上是DFS。
* 中序遍历 
  对于节点的处理工作是在它的左儿子之后，右儿子之前；先遍历左子树，然后访问根节点，然后遍历右子树。实际上是DFS。
  
* 层序遍历 实际上就是广度优先遍历。后面会细说。

## 二叉查找树(binary search tree)
我们一般使用的树，默认为二叉查找树（Binary Search Tree），它的深度的平均值是 **O(logN)** ，最坏的情况下，深度可以达到 **N-1**。
* 注 本节非注明，二叉树代表的就是二叉查找树

二叉树成为二叉查找树最关键的性质就是，对于树中的每个节点X，它的左子树中所有关键字值小于X的关键字值，而它的右子树中所有关键字值大于X的关键字值。注意，这意味着，该树的所有的元素可以用某种统一的方式排序。
由于树的递归定义，我们通常会递归的编写操作的程序，而一般二叉树的深度是O(logN)，所以我们一般不必担心栈空间被用尽。


### AVL树 
AVL(Adelson-Velskii和Landis)树是带有平衡条件的二叉查找树。它的每个节点的左子树和右子树的高度最多差1.

## 如何遍历一棵树
如何遍历一棵树

有两种通用的遍历树的策略：

* 深度优先搜索（DFS）
在这个策略中，我们采用深度作为优先级，以便从跟开始一直到达某个确定的叶子，然后再返回根到达另一个分支。
深度优先搜索策略又可以根据根节点、左孩子和右孩子的相对顺序被细分为先序遍历，中序遍历和后序遍历。

* 宽度优先搜索（BFS）
我们按照高度顺序一层一层的访问整棵树，高层次的节点将会比低层次的节点先被访问到。

下图中的顶点按照访问的顺序编号，按照 1-2-3-4-5 的顺序来比较不同的策略。
![](https://pic.leetcode-cn.com/8e21fed563ab0c9564fb6aaba01934ee6986e0097af51e21e792bee1f4eef4d4-102.png)




# 常见例题
为了节省空间，二叉树定义统一为
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
```
## 二叉树的前序遍历
我们可以最方便的知道，二叉树的表达式是递归表达的。那么最简单的前序遍历也可以使用递归的方法。Top -> Bottom;Left -> Right
```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        dfs(ans,root);
        return ans;
    }
    void dfs(vector<int>& ans,TreeNode* root) {
        if(root==NULL)
            return;
        ans.push_back(root->val);
        dfs(ans,root->left);
        dfs(ans,root->right);
    }
};
```

而非递归的方法就可以使用一个栈来处理。创造一个栈，当根节点不为空时，访问根节点，并入栈；若根节点的左子树不为空，则将左结点置为根节点；若为空，则取栈顶元素，并将栈顶元素的右节点置为根节点，一直到栈为空并且root为空。
```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> nodeStack;
        vector<int> ans;
        while(root || !nodeStack.empty()) {
            //如果根节点存在，则加入栈中
            while(root) {
                nodeStack.push(root);
                ans.push_back(root->val);
                root = root->left;
            }
             //到达左节点为空的时候，直接把栈顶元素取出
            root = nodeStack.top();
            nodeStack.pop();
            //因为左节点为空，那就从右节点开始
            root=root->right;
        }
        return ans;
    }
};
```
## 二叉树的中序遍历
递归法。Left -> Node -> Right
```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        dfs(ans,root);
        return ans;
    }
    void dfs(vector<int>& ans,TreeNode* root) {
        if(root==NULL)
            return;
        dfs(ans,root->left);
        ans.push_back(root->val);
        dfs(ans,root->right);
    }
};
```
迭代，还是使用栈的方法。一直顺着根节点的左结点找下去，直到某个节点的左结点为空，把这个结点的值压栈，然后访问这个节点的右节点。再以同样的方式顺着这个节点的左结点找
```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;    
        stack<TreeNode*> nodeStack;
        while(root || !nodeStack.empty()) {
            while(root) {
                //左节点持续压栈
                nodeStack.push(root);
                root = root->left;
            }
            root = nodeStack.top();
            //当前无左节点，取出值
            ans.push_back(root->val);
            nodeStack.pop();
            root = root->right;
        }   
        return ans;
    }
};
```
## 二叉树的后序遍历
递归
```C++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        dfs(ans,root);
        return ans;
    }
    void dfs(vector<int>& ans,TreeNode* root) {
        if(root == NULL) {
            return;
        }
        dfs(ans,root->left);
        dfs(ans,root->right);
        ans.push_back(root->val);
    }
};
```

迭代法。从根节点开始依次迭代，弹出栈顶元素输出到输出列表中，然后依次压入它的所有孩子节点，按照从上到下、从右至左的顺序依次压入栈中。
因为深度优先搜索后序遍历的顺序是从下到上、从左至右，所以需要将输出列表逆序输出。

```C++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root==NULL) {
            return ans;
        }
        stack<TreeNode*> nodeStack;
        TreeNode *temp = root;
        nodeStack.push(temp);
        while(!nodeStack.empty()) {
            temp = nodeStack.top();
            if(!temp->left && !temp->right) {
                nodeStack.pop();
                ans.emplace_back(temp->val);
            }
            if(temp->right) {
                nodeStack.push(temp->right);
                temp->right = NULL;
            }
            if(temp->left) {
                nodeStack.push(temp->left);
                temp->left = NULL;
            }    
        }
        return ans;
    }
};
```

