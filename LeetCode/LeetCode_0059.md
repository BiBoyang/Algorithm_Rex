
# LeetCode_0059 螺旋矩阵 II

给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

输入: 3
输出:
```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

# 解答
```C++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty() || matrix[0].empty()) {
            return {};
        }
        vector<int> res;
        int height = matrix.size();
        int width = matrix[0].size();
        /*
        left-- 左边界列的纵坐标 right-- 右边界列的纵坐标 
        up -- 上边界行的横坐标 down-- 下边界行的横坐标
        */
        int left = 0,right = width - 1,up = 0, down = height - 1;
        while(true) {
            //left->right
            for(int i = left;i<=right;i++) {
                res.push_back(matrix[up][i]);
            }    
            up++;
            if(up>down) break;
            //up->down
            for(int i = up;i<=down;i++) {
                res.push_back(matrix[i][right]);
            }
            right--;
            if(right<left) break;
            //right->left
            for(int i = right;i>= left;i--) {
                res.push_back(matrix[down][i]);
            }
            down--;
            if(down < up) break;
            //down->up
            for(int i = down;i>= up;i--) {
                res.push_back(matrix[i][left]);
            }            
            left++;
            if(left > right) break;
        }
        return res; 
    }
};
```

* 时间复杂度：O(mn)，其中 m 和 n 分别是输入矩阵的行数和列数。矩阵中的每个元素都要被访问一次。

* 空间复杂度：O(1)。除了输出数组以外，空间复杂度是常数。
