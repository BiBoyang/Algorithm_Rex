# 面试题10- II. 青蛙跳台阶问题
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

# 解法
```C++
class Solution {
public:
    int numWays(int n) {
        vector<int> dp(n+1,1);
        for(int i = 2;i<=n;i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
};
```
