# LeetCode_0113 路径总和II
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

# 解答

 使用递归
```C++
class Solution {
public:
	vector<vector<int>> res;
	vector<int> current_total;
	
	void dfs(TreeNode *root,int sum) {
		if(root == NULL) return ;
		sum = sum - root->val;
		current_total.push_back(root->val);
		if(root->left == NULL && root->right == NULL && sum == 0) {
			res.push_back(current_total);
		}
		if(root->left) dfs(root->left,sum);
		if(root->right) dfs(root->right,sum);

		current_total.pop_back();
	}

    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        if(root) dfs(root,sum);
        return res;
    }
};
```
* 时间复杂度: O(n), 需要访问每一个结点，所以时间复杂度为O(n)
* 空间复杂度: 最好情况，当树是完全二叉树时，递归的深度为log(n), 所以最多需要log(n)的函数调用栈空间；最坏情况，当树退化为链表时，递归的深度为n, 需要n的函数调用中空间。



## 使用栈模拟递归,进行回溯

```C++
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
	    vector<vector<int>> ans; vector<int> curr; //分别记录所有满足条件的路径、一条满足条件的路径
	    if (!root) return ans;
	    stack<TreeNode*> stk; TreeNode *prev = nullptr;
	    while (root || !stk.empty()) { //模拟系统递归栈
		    while (root) {
			    stk.push(root); sum -= root->val; curr.push_back(root->val); //入栈、更新剩余和、路径
			    root = root->left;
	    	}//递归访问左结点
	    	root = stk.top(); //不能再左了，取得右拐点（根结点）
	    	if (!root->left && !root->right && (sum == 0)) { //条件：是叶子结点且剩余和为0
		    	ans.push_back(curr); //满足条件，保存路径
	    	}

		    if (!root->right || root->right == prev) { //右结点不存在或已经访问 回溯
			    stk.pop(); sum += root->val; curr.pop_back(); //出栈、更新剩余和、路径
			    prev = root; //标记已访问
			    root = nullptr; //用于回溯到上一级
		    } else { //递归访问右结点
			    root = root->right;
		    }
	    }
	    return ans;
    }
};
```
* 时间复杂度: O(n), 需要访问每一个结点，所以时间复杂度为O(n)
* 空间复杂度: 最好情况，当树是完全二叉树时，递归的深度为log(n), 所以最多需要log(n)的函数调用栈空间；最坏情况，当树退化为链表时，递归的深度为n, 需要n的函数调用中空间。
