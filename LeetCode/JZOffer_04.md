# 二维数组的查找

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = 5，返回 true。

给定 target = 20，返回 false。

# 解答

右上角标志法

```C++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.size() == 0) return false;

        int rows = matrix.size(),columns = matrix[0].size();
        int rowIndex = 0,colIndex = columns-1;
        while(rowIndex < rows && colIndex >= 0) {
            int num = matrix[rowIndex][colIndex];
            if(num == target) {
                return true;
            } else if(num > target) {
                colIndex--;
            } else {
                rowIndex++;
            }
        }
        return false;;
    }
};
```
时间复杂度：O(n+m)

空间复杂度：O(1)


