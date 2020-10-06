# LeetCode_264 丑数II
编写一个程序，找出第 n 个丑数。

丑数就是只包含质因数 2, 3, 5 的正整数。

示例:

输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。

说明:  

    1 是丑数。
    n 不超过1690。

## 解答
我们将这个问题拆分，


```
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> ugly(n, 1), idx(3, 0);
        for (int i = 1; i < n; ++i){
            int a = ugly[idx[0]]*2, b = ugly[idx[1]]*3, c = ugly[idx[2]]*5;
            int next = min(a, min(b, c));
            if (next == a){
                ++idx[0];
            } 
            if (next == b){
                ++idx[1];
            } 
            if (next == c){
                ++idx[2];
            }
            ugly[i] = next;
        }
        return ugly.back();
    }
};
```