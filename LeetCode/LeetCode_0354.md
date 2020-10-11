# LeetCode_0354 俄罗斯套娃信封问题

给定一些标记了宽度和高度的信封，宽度和高度以整数对形式 (w, h) 出现。当另一个信封的宽度和高度都比这个信封大的时候，这个信封就可以放进另一个信封里，如同俄罗斯套娃一样。

请计算最多能有多少个信封能组成一组“俄罗斯套娃”信封（即可以把一个信封放到另一个信封里面）。

**说明:**
不允许旋转信封。

示例:
```
输入: envelopes = [[5,4],[6,4],[6,7],[2,3]]
输出: 3 
解释: 最多信封的个数为 3, 组合为: [2,3] => [5,4] => [6,7]。
```

# 解答

这道题，实际上是最长递增序列的一个变种。

我们要解决这个问题，要先将进行排序。但是这个排序，我们要细节：
当 w 相同的时候，h 要进行反向排序，即先大后小的排序。

* 如果 w 不相同，则 w 要按照从小到大进行排序，。因为只有 w 从小到大了，可以形成递增序列了，那么这个时候就要去判断 h 的序列就可以了；
* 如果 w 相同，则 h 要按照从大到小进行排序。由于 w 相等，那么只有 h 从大到小排序才不会计算重复的子序列。

然后假设 0 < j < i，设定一个 dp 数组为 1。

只有当 nums[i] > nums[j] 时：nums[i] 才可以接在 nums[j] 后面，形成一个比 dp[j] 更长的上升子序列，长度为 dp[j] + 1。


```C++
class Solution {
public:
    int maxEnvelopes_1(vector<vector<int>>& envelopes) {
        if(envelopes.empty())return 0;
        //先按w排序，若w相同，则按h由高到低排序；若w不同，则按w由小到大排序
        sort(envelopes.begin(),envelopes.end(),[](const vector<int>& a,const vector<int>& b){
            return a[0]<b[0]||(a[0]==b[0]&&a[1]>b[1]);
        });
        int n=envelopes.size(),res=0;
        vector<int> dp(n,1);
        for(int i=0;i<n;++i){
            for(int j=0;j<i;++j){
                if(envelopes[j][1]<envelopes[i][1]){
                    dp[i]=max(dp[i],dp[j]+1);
                }
            }
            res=max(res,dp[i]);
        }
        return res;
    }
}
```
* 时间复杂度：O(n ^ 2)；
* 空间复杂度：O(n)。
