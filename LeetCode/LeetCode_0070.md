# LeetCode_0070 爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：
```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```
示例 2：
```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```
# 解答
# 方法一：和Fib用同样的方法。

```C++
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;

    }
};
```
时间复杂度：O(n)；
空间复杂度：O(1)。
## 方法二：动态规划
我们可以发现，这个问题可以分解成最优子结构的子问题。
发现第i级阶梯可以又两种情况得到：
> * 1. 在第(i-1)阶后向上爬一阶；
> * 2. 在第(i-2)阶后向上爬两阶；

所以到达第i阶的方法就是到达第(i-1)阶和(i-2)阶的方法数之和。
我们可以得到状态转移公式:
* dp[i] = dp[i-1] + dp[i-2] 
 
 ```C++
 class Solution {
public:
    int climbStairs(int n) {
        if(n == 1) return 1;
        vector<int> dp(n+1,-1);
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3;i<=n;i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
};
 ```
 时间复杂度：O(n)。
 空间复杂度：O(1)。
 
## 方法三：斐波那契公式
![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/lc_0070_1.png?raw=true)
公式的计算过程不谈。
```C++
class Solution {
public:
    int climbStairs(int n) {
        const double s = sqrt(5);
        return floor(pow((1+s)/2,n+1)/s + 0.5);
    }
};
```