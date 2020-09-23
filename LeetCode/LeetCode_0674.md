# LeetCode_0674 最长连续递增序列

给定一个未经排序的整数数组，找到最长且连续的的递增序列，并返回该序列的长度。


示例 1:

```
输入: [1,3,5,4,7]
输出: 3
解释: 最长连续递增序列是 [1,3,5], 长度为3。
尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为5和7在原数组里被4隔开。 
```


示例 2:

```
输入: [2,2,2,2,2]
输出: 1
解释: 最长连续递增序列是 [2], 长度为1。
```
 

注意：数组长度不会超过10000。


# 解答

dp[i] 表示位置 i 的连续递增子序列长度，初始化为 1，因为每个数字是最小的递增子序列为 1.

则状态转移方程为：

<!--
$ dp[i]
  \begin{cases}
  dp[i-1]+1  &nums[i-1] < nums[i]\\
  dp[i] = 1  &nums[i-1] \geq\ nums[i]\\
  \end{cases}$
  -->

![](https://github.com/BiBoyang/Algorithm_Rex/blob/master/Image/leetcode_0674_00.png?raw=true)


```C++
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        int len = nums.size();
        int res = 1;
        if(len == 0) return 0;
        vector<int> dp(len,1);
        for(int i = 1;i < len;i++) {
            if(nums[i - 1] < nums[i]) {
                dp[i] = dp[i - 1] + 1;
            }
            res = max(res,dp[i]);
        }
        return res;
    }
};
```

