# LeetCode_647 回文子串
给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。

示例 1:
```
输入: "abc"
输出: 3
解释: 三个回文子串: "a", "b", "c".
```
示例 2:
```
输入: "aaa"
输出: 6
说明: 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".
```

注意:
* 输入的字符串长度不会超过1000。

## 解答
状态转移
> if （str[i]==str[j]）
> dp[i][j] = dp[i+1][j] + dp[i][j-1]+1  

> if（str[i]！=str[j]）
> dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1]


```
class Solution {
public:
    int countSubstrings(string s) {
        int len = s.length();
        if(len == 0) return 0;
        vector<int> f(len,0); //记录以每个字母为底的字符串的回文序个数
        vector<vector<int> > dp(len, vector<int>(len));  //(j,i)是否为回文
        f[0] = 1;
        for(int i = 0;i<len;i++) 
            dp[i][i]=1;
        for(int i = 1;i<len;i++) {
            int num = 1;
            for(int left = i - 1;left >= 0;left--) {
                /*
                * 这里要注意，不要贴近连续两个数字,
                * 因为连续几个相同的数字有可能直接构成回文，而不必参考[left+1][i-1]
                */
                if((left+1) < (i-1)) {
                    if(s[left] == s[i] && dp[left+1][i-1]) {
                        num++;
                        dp[left][i] = 1;
                    } else {
                        dp[left][i] = 0;
                    }
                } else if(s[left]==s[i]) {
                    //这里是为了处理连续相同的数字，比如说aaab
                    // num++;
                    dp[left][i] = 1;
                } else { 
                    dp[left][i] = 0;
                }
            }
            f[i]=f[i-1]+num;
        }
        return f[len-1];
    }
};
```
