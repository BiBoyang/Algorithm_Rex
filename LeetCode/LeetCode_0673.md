# LeetCode_0673 最长递增子序列的个数 🚧

给定一个未排序的整数数组，找到最长递增子序列的个数。

示例 1:
```
输入: [1,3,5,4,7]
输出: 2
解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。
```
示例 2:
```
输入: [2,2,2,2,2]
输出: 5
解释: 最长递增子序列的长度是1，并且存在5个子序列的长度为1，因此输出5。
```
注意: 给定的数组长度不超过 2000 并且结果一定是32位有符号整数。


# 解答

这道题可以使用 线性动态规划。

用 dp[i] 表示以 nums[i] 为结尾的递推序列的长度，用cnt[i]表示以nums[i]为结尾的递推序列的个数，初始化都赋值为1，只要有数字，那么至少都是1。





```C++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        if (nums.empty()) return 0;
        int N = nums.size();
        // pair<int, int> 分别为最长递增长度与对应的数目
        vector<pair<int, int> > dp(N, {1, 1});
        int mx = 1;
        for (int i = 1; i < N; ++i) {
            for (int j = 0; j < i; ++j) {
                if (nums[i] > nums[j]) {
                    if (dp[i].first < dp[j].first + 1) {
                        dp[i] = {dp[j].first + 1, dp[j].second};
                    } else if (dp[i].first == dp[j].first + 1) {
                        dp[i].second += dp[j].second;
                    }
                }
            }
            mx = max(mx, dp[i].first);
        }
        int res = 0;
        for (int i = 0; i < N; ++i) {
            if (dp[i].first == mx) {
                res += dp[i].second;
            }
        }
        return res;
    }
};

```



还有 贪心算法、树状动态规划方法

