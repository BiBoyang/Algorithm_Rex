# 面试题29. 顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 

示例 1：
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

示例 2：
```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

# 解答

```C++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty() || matrix[0].empty())return {};
        int high = matrix.size();
        int width = matrix[0].size();
        vector<int> res;
        int up = 0,down = high - 1,left = 0,right = width - 1;
        while(true) {
            //左上->右上
            for(int i = left;i <= right;i++) {
                res.push_back(matrix[up][i]);
            }
            up++;
            if(up > down) break;

            //右上->右下
            for(int i = up;i<=down;i++) {
                res.push_back(matrix[i][right]);
            }
            right--;
            if(left>right) break;

            //右下->左下
            for(int i = right;i >= left;i--) {
                res.push_back(matrix[down][i]);
            }
            down--;
            if(up > down) break;

            //左下->左上
            for(int i = down;i>= up;i--){
                res.push_back(matrix[i][left]);
            }
            left++;
            if(left>right) break;
        }
        return res;
    }
};
```
* 时间复杂度 O(MN) ： M,N 分别为矩阵行数和列数。
* 空间复杂度 O(1)