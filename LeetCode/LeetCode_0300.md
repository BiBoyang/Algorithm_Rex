# LeetCode_0300 最长上升子序列🚧

给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例:
```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```
说明:
* 可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
* 你算法的时间复杂度应该为 O(n2) 。

进阶: 你能将算法的时间复杂度降低到 O(n log n) 吗?

# 解答
## 动态规划
设定：dp[i] 代表以 nums[i] 结尾的 LIS 的长度；

状态转移方程：
<!--dp[i] = max(dp[j] + 1,dp[i])  if(1 <= j <  i，nums[j] < nums[i])-->
<!--$ dp[i] = 
  \begin{cases}
  max(dp[j] + 1,dp[i])  &if(1 <= j <  i，nums[j] < nums[i])\\
  \end{cases}$-->

![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/leetcode_0300.png?raw=true)



```C++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        int ans = 1;
        vector<int>dp(nums.size(),1);
        for(int i = 1;i < nums.size();i++) {
            for(int j = 0;j < i;j++) {
                if(nums[j] < nums[i]) {
                    dp[i] = max(dp[i],dp[j]+1);
                    ans = max(dp[i],ans);
                }
            }
        }
        return ans;
    }
};
```

* 时间复杂度：O(n^2 );
* 空间复杂度：O(n)