# LeetCode_240 搜索二维矩阵 II

编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：
> * 每行的元素从左到右升序排列。
> * 每列的元素从上到下升序排列。

**示例:**

>现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。
给定 target = 20，返回 false。

## 答案
右上角法
```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(!matrix.empty()) {
            //行列个数
            int row = matrix.size();
            int col = matrix[0].size();
            //右上角坐标
            int a = 0;
            int b = col - 1;
            
            while(a < row && b >= 0) {
                //当前数组就是目标数字
                if(matrix[a][b] == target) {
                    return true;
                }
                //不是当前数字继续查找
                if(matrix[a][b] < target) {
                    a++;
                }else {
                    b--;
                }   
            }  
        }
        return false;
    }
};

```
