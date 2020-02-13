
# LeetCode_0987 二叉树的垂序遍历

给定二叉树，按垂序遍历返回其结点值。

对位于 (X, Y) 的每个结点而言，其左右子结点分别位于 (X-1, Y-1) 和 (X+1, Y-1)。

把一条垂线从 X = -infinity 移动到 X = +infinity ，每当该垂线与结点接触时，我们按从上到下的顺序报告结点的值（ Y 坐标递减）。

如果两个结点位置相同，则首先报告的结点值较小。

按 X 坐标顺序返回非空报告的列表。每个报告都有一个结点值列表。

# 解答
这道题看起来很复杂，但是其实用DFS就可以了。
我们可以使用哈希表来存储结果值和层级。

```C++
class Solution {
public:
    map<int, vector< pair<int, int> > > memo;
    void dfs(TreeNode* root, int x, int y) {
        if (root == NULL) return;
        memo[x].push_back({y, root->val});
        dfs(root->left, x - 1, y + 1);
        dfs(root->right, x + 1, y + 1);
    }
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        dfs(root, 0, 0);
        vector<vector<int> > res;
        for (auto& p : memo) {
            sort(p.second.begin(), p.second.end());
            vector<int> v;
            for (auto t : p.second) {
                v.push_back(t.second);
            }
            res.push_back(v);
        }
        return res;
    }
};
```