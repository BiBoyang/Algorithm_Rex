
# LeetCode_0559 N叉树的最大深度

给定一个 N 叉树，找到其最大深度。

最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。

# 解答
## 方法一：递归
```C++
class Solution {
public:
    int maxDepth(Node* root) {
        int deep = 0;
        if(root == NULL) {
            return 0;
        } else {
            for(auto temp: root->children) {
                if(temp) {
                    deep = max(deep,maxDepth(temp));
                }
            }
        }
        return deep + 1;
    }
};
```
时间复杂度：O(n)。
空间复杂度：最差O(n)，最好（树完全平衡）是O(logN)。


