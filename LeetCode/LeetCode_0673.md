# LeetCode_0673 最长递增子序列的个数

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

用 dp[i] 表示以 nums[i] 为结尾的递推序列的长度，用cnt[i]表示以nums[i]为结尾的递推序列的个数，初始化都赋值为1，只要有数字，那么至少都是1。

然后遍历数组，对于每个遍历到的数字 nums[i] ，我们再遍历其之前的所有数字 nums[j]，当 nums[i] 小于等于 nums[j] 时，不做任何处理，因为不是递增序列。反之，则判断 dp[i] 和 dp[j] 的关系，如果 dp[i] 等于 dp[j] + 1，说明 nums[i] 这个数字可以加在以 nums[j] 结尾的递增序列后面，并且以 nums[j] 结尾的递增序列个数可以直接加到以 nums[i] 结尾的递增序列个数上。如果 dp[i] 小于 dp[j] + 1，说明我们找到了一条长度更长的递增序列，那么我们此时将 dp[i] 更新为 dp[j]+1，并且原本的递增序列都不能用了，直接用cnt[j]来代替。

维护一个全局最长的子序列长度mx，每次都进行更新，到最后遍历一遍每个节点，如果长度等于 mx,res+=cnt[i];

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



