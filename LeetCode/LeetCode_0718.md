# LeetCode_0718 最长重复子数组
给两个整数数组 A 和 B ，返回两个数组中公共的、长度最长的子数组的长度。

 

示例：
```
输入：
A: [1,2,3,2,1]
B: [3,2,1,4,7]
输出：3
解释：
长度最长的公共子数组是 [3, 2, 1] 。
```

提示：

* 1 <= len(A), len(B) <= 1000
* 0 <= A[i], B[i] < 100

# 解答
最开始想暴力解法。
```C++
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        int res = 0;
        for(int i = 0;i < A.size();i++) {
            for(int j = 0;j<B.size();j++) {
                int k = 0;
                while(A[i+k] == B[j+k]) {
                    k++;
                }
                res = max(res, k);
            }
        }
        return res;
    }
};
```

我们可以知道，这个方法的时间复杂度是O(n * n * n)。时间复杂度很高，我们可以从这个方法开始推导出其他更加优秀的方法。


## 动态规划

假设 A 数组为[1,2,3], B 数组为[1,2,4]。我们可以理解，A[0] 和 B[0] 是相同的，可以记为 1 ，而如果后续的 A[1] 和 B[1] 也是相同，计数为 2，而 A[2] 和 B[2] 是不同的，则最终记为 2。

我们可以发现，实际上，对于 i 位的相同数字的长度，实际上取决于它的下一位，即 i+1 位。

我们可以推导出状态方程；

* 如果 A[i] == B[j]
        则 dp[i][j] = dp[i+1][j+1] + 1;
* 如果 A[i] != B[j]
        则 dp[i][j] = 0。 
        
```C++
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        int lenA = A.size(),lenB = B.size(),ans = 0;
        vector<vector<int>> dp(lenA + 1,vector<int>(lenB + 1,0));
        for(int i = lenA - 1;i>=0;i--){
            for(int j = lenB-1;j>=0;j--) {
                if(A[i] == B[j]) {
                    dp[i][j] = dp[i+1][j+1] + 1;
                } else {
                    dp[i][j] = 0;
                }
                ans = max(ans, dp[i][j]);
            }
        }
        return ans;
    }
};
```