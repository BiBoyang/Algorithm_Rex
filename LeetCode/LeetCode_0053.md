# LeetCode_0053 最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:
```
输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

# 解答


这道题的算法很简单。

对于一个连续子数组的最大和，假设为 dp[i],则
dp[i] = max(dp[i] + nums[i],nums[i])。



```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int len = nums.size();
        if(len == 0) return 0;
        if(len == 1) return nums[0];
        
        vector<int> dp(len);
        dp[0] = nums[0];
        int res = dp[0];
        
        for(int i = 1;i < len;i++) {
            dp[i] = max(dp[i - 1] + nums[i],nums[i]);
            res = max(dp[i],res);
        }
        return res;

    }
};
```