
# LeetCode_0001 两数之和

给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:
```
输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]
```

示例 2:

```
输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]
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