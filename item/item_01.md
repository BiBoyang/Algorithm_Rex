# 螺旋矩阵三连
螺旋矩阵是几道题是很有趣的题，考察程序员对于边界的处理和敏感度。
思路很好解决，但是如果要真正的写出无bug的代码实际上还是有点难度--这个难度在于边界的处理，我最开始解决问题的时候，伪代码一下写了出来，但是真正运行没问题的代码却写了很长时间。尤其是第三题，简直是一种折磨。

先看第一道螺旋矩阵（一）。

## 螺旋矩阵（一）
给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:

> **输入:**
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
**输出:** [1,2,3,6,9,8,7,4,5]

示例 2:

> **输入:**
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
**输出:** [1,2,3,4,8,12,11,10,9,5,6,7]

### 解答思路：
明确一下思路，我们是要螺旋的顺时针的访问元素。
![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/luoxuan_01.png?raw=true)

这个图看起来还是有点迷糊，我们把每个点的坐标画出来，就更加明白了。
![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/luoxuan_02.png?raw=true)

首先，我们一定要明确每一步的上下左右边界。

然后首先在第一行向右开始遍历，到了最右之后，就从上而下，这个时候我们要把起始高度变为这一行的高度；依次类推。
注意，我们的边界条件有四种
> * 1.从上边界开始的边界**up**大于下边界**down**；
> * 2.从右边界开始的边界**right**小于左边界**left**；
> * 3.从下边界开始的边界**down**小于上边界**up**；
> * 4.从左边界开始的边界**left**大于右边界**right**；


代码演示如下：
```C++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty() || matrix[0].empty()) {
            return {};
        }
        int height = matrix.size(), width = matrix[0].size();
        vector<int> res;
        int up = 0, down = height - 1, left = 0, right = width - 1;
        
        while (true) {
            //从左往右
            for(int i = left;i<=right;i++) {
               res.push_back(matrix[up][i]);
            }
            //上面大于下面
            up++;
            if(up > down)break;
            
            //从右上往右下
            for(int i=up;i<=down;i++) {
                res.push_back(matrix[i][right]);
            }
            //右边小于左边
            right--;
            if(right < left) break;
            
            //从右下往左下
            for(int i=right;i>=left;i--) {
                res.push_back(matrix[down][i]);
            }
            //下边小于上面
            down--;
            if(down < up) break;
            
            //从左下往左上
            for(int i=down;i>=up;i--) {
                res.push_back(matrix[i][left]);
            }
            //左边超过了右边
            left++;
            if(left > right)break;
        }
        return res;
    }
};
```

## 螺旋矩阵（二）
给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

> **输入**: 3
**输出**:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

### 解答思路：
这道题实际上和上一道题非常的想象。
上一道题是螺旋的输出数字，而这个是不停的输入数字。
很多代码甚至能直接从上一题套用过来。
```C++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        if(n==0) {
            return vector<vector<int>>();
        }
        vector<vector<int>> mat(n,vector<int>(n,0));

        int up=0,down = n-1,left = 0,right = n-1;
        int k = 0;
        
        int num = 1, target = n * n;
        while(num <= target){
            //left-->right 
            for(int i = left; i <= right; i++) {
                mat[up][i] = num++; // left to right.
            }
            up++;
            //up-->down
            for(int i = up; i <= down; i++) {
                mat[i][right] = num++; // top to bottom.
            }
            right--;
            //right-->left
            for(int i = right; i >= left; i--) {
                mat[down][i] = num++; // right to left.
            }
            down--;
            //down-->up
            for(int i = down; i >= up; i--) {
                mat[i][left] = num++; // bottom to top.
            }
            left++;
        }
        return mat;
    }
};
```

## 螺旋矩阵（三）
在 R 行 C 列的矩阵上，我们从 `(r0, c0)` 面朝东面开始。
这里，网格的西北角位于第一行第一列，网格的东南角位于最后一行最后一列。
现在，我们以顺时针按螺旋状行走，访问此网格中的每个位置。
每当我们移动到网格的边界之外时，我们会继续在网格之外行走（但稍后可能会返回到网格边界）。
最终，我们到过网格的所有 R * C 个空间。
按照访问顺序返回表示网格位置的坐标列表

**示例 1：**
> 输入：R = 1, C = 4, r0 = 0, c0 = 0
输出：[[0,0],[0,1],[0,2],[0,3]]
![](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/08/24/example_1.png)



**示例 2：**
> 输入：R = 5, C = 6, r0 = 1, c0 = 4
输出：[[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]
![](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/08/24/example_2.png)

#### 解答思路

我刚刚看到这道题的时候，我花了五分钟没有读懂题。😓
然后我对着示例二的图画了好一阵，才大概明白题意。我估计面试是肯定不会出这种题的，估计光看题就能绕死一堆人。



这道题的思路在于，要先忽略是否在网格之中。先去进行顺时针的螺旋形状行走，然后在结果中判断是否在网格中。

这道题的代码量很大，而且处处都会出错，我最开始即使在领会了思路的前提下，依然花了很长的时间才写出代码。
> * 吐个槽，这道题即使再给我出，我估计也很难在短时间内写出bugfree的代码。

```C++
class Solution {
public:
    vector<vector<int>> spiralMatrixIII(int R, int C, int r0, int c0) {
        /*已经过的个数*/
        int num = 1;
        vector<vector<int>> p;
        vector<int> temp(2);
        temp[0] = r0;
        temp[1] = c0;
        p.push_back(temp);
        /*移动步长*/
        int step = 1;
        while(num < R * C) {
            /*朝东走*/
            int n = 1;
            while(n <= step) {
                c0++;
                if(Judge(r0, c0, R, C))
                {
                    temp[0] = r0;
                    temp[1] = c0;
                    p.push_back(temp);
                    num++;
                }
                n++;
            }
        
            /*朝南走*/
            n = 1;
            while(n <= step) {
                r0++;
                if(Judge(r0, c0, R, C)) {
                    temp[0] = r0;
                    temp[1] = c0;
                    p.push_back(temp);
                    num++;
                }
                n++;
            }
        
            /*步长加1*/
            step++;
        
            /*朝西走*/
            n = 1;
            while(n <= step) {
                c0--;
                if(Judge(r0, c0, R, C)) {
                    temp[0] = r0;
                    temp[1] = c0;
                    p.push_back(temp);
                    num++;
                }
                n++;
            }
        
            /*朝北走*/
            n = 1;
            while(n <= step) {
                r0--;
                if(Judge(r0, c0, R, C)) {
                    temp[0] = r0;
                    temp[1] = c0;
                    p.push_back(temp);
                    num++;
                }
                n++;
            }
            /*步长加1*/
            step++;
        }
        return p;    
    }
        /*判断是否在规定区域内*/
    bool Judge(int x, int y, int r, int c) {
        if(x >= 0 && y >=0 && x < r && y < c) {
            return true;
        } else {
            return false;
        }        
    }
};
```