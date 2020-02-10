
# LeetCode_0098 验证二叉搜索树
给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

* 节点的左子树只包含小于当前节点的数。
* 节点的右子树只包含大于当前节点的数。
* 所有左子树和右子树自身必须也是二叉搜索树。

# 解答
## 解法一

记录父节点的值是否在子节点的区间内
代码一：
```C++
class Solution {
public:
    long last = LONG_MIN; // 父节点值
    bool flag = true; // 父亲结点是否大于子节点
    bool isValidBST(TreeNode* root) {
        if(!root) {
            return true;
        }
        
        // 遍历左子树
        if(flag && root->left) {
            isValidBST(root->left);
        }
        
        // 当前结点不大于父节点，不是排序二叉树
        if(root->val <= last) {
            flag = false;
        }
        
        last = root->val; // 记录父节点值
        // 遍历右子树
        if(flag && root->right) {
            isValidBST(root->right);
        }
        
        // 子树都遍历完 或 不是二叉排序树，就退出
        return flag;
    }
};
```
代码二：
```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return dfs(root,INT_MIN,INT_MAX);
    }
    bool dfs(TreeNode *node,long long minV, long long maxV) {
        if(!node) return true;
        if(node->val < minV || node->val > maxV) return false;
        return dfs(node->left,minV,node->val - 1ll) && dfs(node->right,node->val+ 1ll,maxV);
    }
};
```

## 解法二
我们这里要知道一个结论。
因为中序遍历的遍历顺序是：左子节点->根节点->右子节点。
所以，二叉搜索树的中序遍历必然是严格递增的。
```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        vector<int> res;
		if(root == NULL) {
            return true;
		} else {
			inorderTraversal(root,res);
			if(res.size()==1){ 
				return true;
            }
			for(int i=0;i<res.size()-1;i++){
				if(res[i] >= res[i+1]) {
					return false;
                }
			}
			return true;
		}
    }
    void inorderTraversal(TreeNode* root,vector<int>& res) {
        if(!root) return;
        inorderTraversal(root->left,res);
        res.push_back(root->val);
        inorderTraversal(root->right,res);
    }
};
```


