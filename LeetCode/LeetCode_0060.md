# LeetCode_0060 第k个排列

给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"
给定 n 和 k，返回第 k 个排列。

说明：

* 给定 n 的范围是 [1, 9]。
* 给定 k 的范围是[1,  n!]。

示例 1:
```
输入: n = 3, k = 3
输出: "213"
```
示例 2:
```
输入: n = 4, k = 9
输出: "2314"
```


# 解答
```C++
class Solution {
public:
    string getPermutation(int n, int k) {
        string res;
        string num = "123456789";
        vector<int>f(n,1);
        //求n!
        for(int i = 1;i< n;i++) {
            f[i] =  f[i-1] * i;
        }
        int temp = k-1;
        for(int i = n;i>=1;--i) {
            int j = temp / f[i-1];
            temp %= f[i-1];
            res.push_back(num[j]);
            num.erase(j,1);
        }
        return res;
    }
};
```