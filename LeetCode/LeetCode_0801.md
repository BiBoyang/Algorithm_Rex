# LeetCode_801 使序列递增的最小交换次数
我们有两个长度相等且不为空的整型数组 A 和 B 。

我们可以交换 A[i] 和 B[i] 的元素。注意这两个元素在各自的序列中应该处于相同的位置。

在交换过一些元素之后，数组 A 和 B 都应该是严格递增的（数组严格递增的条件仅为A[0] < A[1] < A[2] < ... < A[A.length - 1]）。

给定数组 A 和 B ，请返回使得两个数组均保持严格递增状态的最小交换次数。假设给定的输入总是有效的。

示例:
```
输入: A = [1,3,5,4], B = [1,2,3,7]
输出: 1
解释: 
交换 A[3] 和 B[3] 后，两个数组如下:
A = [1, 3, 5, 7] ， B = [1, 2, 3, 4]
两个数组均为严格递增的。
```

注意:

* A, B 两个数组的长度总是相等的，且长度的范围为 [1, 1000]。
* A[i], B[i] 均为 [0, 2000]区间内的整数。

## 解答
由于题目保证一定有正确答案，所以以下两种可能性会至少满足一个。

> 1. **A[i] > A[i - 1] && B[i] > B[i - 1]**：这说明在维持第i对元素和第i - 1对元素同序的情况下可以满足条件，所以我们可以让dp1[i]和dp2[i]分别从INT_MAX降低到dp1[i - 1]和dp2[i - 1] + 1，也就是如果A[i - 1]和B[i - 1]交换了，那么我们也让A[i]和B[i]也交换；如果A[i - 1]和B[i - 1]维持原序，那么我们也让A[i]和B[i]维持原序。

> 2. **B[i] > A[i - 1] && A[i] > B[i - 1]**：这说明维护第i对元素和第i - 1对元素反序的情况下也可以满足条件，所以我们就看看能不能进一步降低dp1[i]和dp2[i]的数组：如果dp2[i - 1] < dp[i]，那么说明交换第i - 1对元素之后，保持第i对元素的次序可以达到更优解；如果dp1[i - 1] + 1 < dp2[i]，那么说明在维持第i - 1对元素的次序的情况下，交换第i对元素可以达到更优解。
```
class Solution {
public:
    int minSwap(vector<int>& A, vector<int>& B) {
        /*
        * dp1[i]表示在不交换i的情况下，使得A的前i + 1个元素和B的前i + 1个元素严格递增的最小交换次数
        * dp2[i]表示在交换i的情况下，使得A的前i + 1个元素和B的前i + 1个元素严格递增的最小交换次数
        */
        int length = A.size();
        vector<int> dp1(length,INT_MAX);
        vector<int> dp2(length,INT_MAX);
        dp1[0] = 0,dp2[0] = 1;
        
        for (int i = 1; i < A.size(); i++) { 
            if (A[i - 1] < A[i] && B[i - 1] < B[i]) {
                 //表示i-1如果没有交换，则i也不交换
                 dp1[i] = dp1[i - 1];
                 //表示i-1交换了，i也交换
                 dp2[i] = dp2[i - 1] + 1;
            } 
            if (A[i - 1] < B[i] && B[i - 1] < A[i]) { 
                //表示dp2在i之前的元素之和
                dp1[i] = min(dp1[i],dp2[i-1]);    
                //表示经过了翻转次数加一
                dp2[i] = min(dp2[i],dp1[i-1] + 1);           
            } 
         } 
        return min(dp1[length - 1], dp2[length - 1]);
    }
};
```