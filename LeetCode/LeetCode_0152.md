# LeetCode_152 乘积最大子组数

给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

 

示例 1:
```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```
示例 2:
```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```


# 解答
解法和第 53 题， 最大子序和有些类似。

最开始可能会按照最大子序和的方式，使用状态转移方程 dp[i] = max(dp[i] + nums[i],nums[i]) 来求得结果，但是这个结果是有一个非常大的缺点的：没有考虑到负数的情况，有时候本来是一个负数的时候，乘以一个负数就会变得最大，所以我们要做两套方案来准备。

分别设置两个动态规划数组，maxDP 和 minDP，分别进行记录结果。则状态转移方程变成了
* maxDP[i] = max( max (maxDP[i - 1] * nums[i],nums[i]),minDP[i - 1] * nums[i]);
* minDP[i] = min( min (maxDP[i - 1] * nums[i],nums[i]),minDP[i - 1] * nums[i]);

就可以解决了。

```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int len = nums.size();
        if(len == 0) return 0;
        int res = nums[0];
        vector<int> maxDP(len);
        vector<int> minDP(len);
        maxDP[0] = nums[0];
        minDP[0] = nums[0];

        for(int i = 1;i < len;i++) {
            maxDP[i] = max( max (maxDP[i - 1] * nums[i],nums[i]),minDP[i - 1] * nums[i]);
            minDP[i] = min( min (maxDP[i - 1] * nums[i],nums[i]),minDP[i - 1] * nums[i]);
            res = max(maxDP[i],res);
        }

        return res;
    }
};
```

* 时间复杂度：O(n)；
* 空间复杂度：O(n)。
