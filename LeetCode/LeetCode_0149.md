# LeetCode_0149. 直线上最多的点数

给定一个二维平面，平面上有 n 个点，求最多有多少个点在同一条直线上。

示例 1:
```
输入: [[1,1],[2,2],[3,3]]
输出: 3
解释:
^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```
示例 2:
```
输入: [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
输出: 4
解释:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```

# 解答

这道题给了一个二维数组，里面的数组指代坐标。我们可以知道，至少不相同的两点，就可以确定一条直线。

那么，我们可以直接计算两个点之间的斜率，然后查看相同斜率的点是否共线。

但是还有两点特殊情况需要考虑，
1. 当两个点重合时，无法确定一条直线，但这也是共线的情况；
2. 由于两个点 (x1, y1) 和 (x2, y2) 的斜率k表示为 (y2 - y1)/(x2 - x1)，那么当 x1 = x2 时斜率不存在（也就是说这条线是垂直的），这种共线情况需要特殊处理。

但是当我正常去计算的时候，即使是使用 float，也是会发生精度问题，那么我们该如何解决呢？

可以使用最大公约数来进行计算，把除数和被除数都保存下来，不做除法，但是要让这两数分别除以它们的最大公约数，这样例如8和4，4和2，2和1，这三组商相同的数就都会存到一个映射里面。

```C++
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int res = 0;
        int len = points.size();
        for(int i = 0;i < len;i++) {
            map<pair<int,int>,int> map;
            int duplicate = 1;//表示重合
            for(int j = i + 1;j < len;j++){
                if(points[i][0] == points[j][0] && points[i][1] == points[j][1]){
                    duplicate++;
                    continue;
                }
                int dx = points[j][0] - points[i][0];
                int dy = points[j][1] - points[i][1];
                int d = gcd(dx,dy);
                map[{dx / d,dy / d}]++;
            }
            res = max(res,duplicate);
            for(auto it = map.begin();it != map.end();it++){
                res = max(res,it->second + duplicate);
            }
            
        }
        return res;
    }
    int gcd(int a, int b) {
        if(b == 0) {
            return a;
        } else {
            return gcd(b, a % b);
        }
    }
};
```