# LeetCode_0885 螺旋矩阵 III

在 R 行 C 列的矩阵上，我们从 (r0, c0) 面朝东面开始

这里，网格的西北角位于第一行第一列，网格的东南角位于最后一行最后一列。

现在，我们以顺时针按螺旋状行走，访问此网格中的每个位置。

每当我们移动到网格的边界之外时，我们会继续在网格之外行走（但稍后可能会返回到网格边界）。

最终，我们到过网格的所有 R * C 个空间。

按照访问顺序返回表示网格位置的坐标列表。

# 解答
```C++
class Solution {
public:

    bool isInArea(int a,int b,int r,int c) {
        if(a >= 0 && b >= 0 && a < r && b < c) {
            return true;
        } else {
            return false;
        }
    }
    vector<vector<int>> spiralMatrixIII(int R, int C, int r0, int c0) {
        int total = 1;
        vector<vector<int>> res;
        vector<int> temp(2);
        temp[0] = r0;
        temp[1] = c0;
        res.push_back(temp);

        int step = 1;//每一轮移动的步长

        while(total < R * C) {
            
            //向东走
            int n = 1;
            while(n <= step) {
                c0++;
                if(isInArea(r0, c0, R, C)){
                    temp[0] = r0;
                    temp[1] = c0;
                    res.push_back(temp);
                    total++;
                }
                n++;
            }

            //向南走
            n = 1;
            while(n <= step) {
                r0++;
                if(isInArea(r0, c0, R, C)){
                    temp[0] = r0;
                    temp[1] = c0;
                    res.push_back(temp);
                    total++;
                }
                n++;
            }

            step++;
            //向西走
            n = 1;
            while(n <= step) {
                c0--;
                if(isInArea(r0, c0, R, C)){
                    temp[0] = r0;
                    temp[1] = c0;
                    res.push_back(temp);
                    total++;
                }
                n++;
            }

            //向北走
            n = 1;
            while(n <= step) {
                r0--;
                if(isInArea(r0, c0, R, C)){
                    temp[0] = r0;
                    temp[1] = c0;
                    res.push_back(temp);
                    total++;
                }
                n++;
            }
            step++;
        }
        return res;
    }
};
```

![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/item_003.png?raw=true)