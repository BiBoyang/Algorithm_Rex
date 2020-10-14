# LeetCode_0918 环形子数组的最大和

给定一个由整数数组 A 表示的环形数组 C，求 C 的非空子数组的最大可能和。

在此处，环形数组意味着数组的末端将会与开头相连呈环状。（形式上，当0 <= i < A.length 时 C[i] = A[i]，且当 i >= 0 时 C[i+A.length] = C[i]）

此外，子数组最多只能包含固定缓冲区 A 中的每个元素一次。（形式上，对于子数组 C[i], C[i+1], ..., C[j]，不存在 i <= k1, k2 <= j 其中 k1 % A.length = k2 % A.length）

 

示例 1：
```
输入：[1,-2,3,-2]
输出：3
解释：从子数组 [3] 得到最大和 3
```
示例 2：
```
输入：[5,-3,5]
输出：10
解释：从子数组 [5,5] 得到最大和 5 + 5 = 10
```
示例 3：
```
输入：[3,-1,2,-1]
输出：4
解释：从子数组 [2,-1,3] 得到最大和 2 + (-1) + 3 = 4
```
示例 4：
```
输入：[3,-2,2,-3]
输出：3
解释：从子数组 [3] 和 [3,-2,2] 都可以得到最大和 3
```
示例 5：
```
输入：[-2,-3,-1]
输出：-1
解释：从子数组 [-1] 得到最大和 -1
```

# 解答

对于整道题，我们要首先理解一个求最大子段和的 Kadane 算法。

如果假定 dp[i] 为以 nums[i] 为结尾的最大子段和。也就是
`dp[j]= max(nums[i] + nums[i+1] +⋯+ nums[j])`

那么说，nums[j+1] 最大字段和应该取决于 nums[j+1] 的大小。即：
`dp[j+1] = nums[j+1] + max(dp[j],0)`

可以写作代码：
```C++
vector<int> dpA(A.size());
dpA[0] = A[0];
for(int i = 1;i < A.size();i++) {
    dpA[i] = A[i] + max(dpA[i-1],0);
    ans = max(ans,dpA[i]);
}
```

这里，为了节约空间复杂度，我们可以进一步演化，将 dpA 数组变成一个变量。
```C++
cur = cur = A[0];
for(int i = 1;i < A.size();i++) {
    cur = A[i] + max(cur,0);
    ans = max(ans,cur);
}
``` 

然后回到问题上。

可以发现，这个问题实际上有两种情况。
1. 这个最大和的子数组在一个区间里；
2. 这个最大和的子数组在两个区间里。

对于情况 1，我们可以直接使用 Kadane 算法来解决。

对于情况 2，可以继续将子段分为两部分，即 包括 nums[len - 1] 在内的左区间，以及以外的右区间。

右区间实际上是求以 nums[0] 为开头的子段和，也是很简单的
```C++
int leftSum = 0;
for (int i = 0; i < len-2; ++i) {
    leftMax += A[i];
    ......
}
```

那么还剩下最后一块，即这个子段的左区间，它是包含 nums[len-1] 的，额外的元素一定在它的左侧，则这段变成了求以 nums[len-1] 为结尾的子段和。当然，还有一个限制条件： **子数组最多只能包含固定缓冲区 A 中的每个元素一次。**

我们先创建一个 rightSums，用以保存左区间里的以 nums[len-1] 结尾的每一段的和；然后在计算出这里面最大的那个并保存。




```C++
class Solution {
public:
    int maxSubarraySumCircular(vector<int>& A) {
        int len = A.size();
        int ans = A[0],cur = A[0];
        //单区间
        for(int i = 1;i < len;i++) {
            cur = A[i] + max(cur,0);
            ans = max(ans,cur);
        }
        //双区间，左右以子段为标准
        vector<int> leftSums(len);
        leftSums[len-1] = A[len-1];
        vector<int> leftMax(len);
        leftMax[len-1] = A[len-1];

        for(int i = len -2;i >=0;i--){
            leftSums[i] = leftSums[i+1] + A[i];
            leftMax[i] = max(leftMax[i+1],leftSums[i]);
        }

        int rightSum = 0;
        for (int i = 0; i < len-2; ++i) {
            rightSum += A[i];
            ans = max(ans, rightSum + leftMax[i+2]);
        }
        return ans;


    }
};
```

* 时间复杂度：O(n)。n 是 A 的长度。
* 空间复杂度：O(n)
