# LeetCode_0074. 搜索二维矩阵
* 二分查找

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。
示例 1:
```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true
```
示例 2:
```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false
```

# 解答

```C++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.size() == 0 || matrix[0].size() == 0) 
            return false;
        int a = matrix.size(), b = matrix[0].size(), left = 0, right = a * b - 1;	
        //二分查找目标值
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (target < matrix[mid / b][mid % b])
                right = mid - 1;
            else if (target > matrix[mid / b][mid % b]) 
                left = mid + 1;
            else 
                return true;
        }
        return false;
    }
};
```
