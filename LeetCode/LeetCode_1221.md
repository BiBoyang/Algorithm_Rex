# LeetCode_1221. 分割平衡字符串

在一个 平衡字符串 中，'L' 和 'R' 字符的数量是相同的。

给你一个平衡字符串 s，请你将它分割成尽可能多的平衡字符串。

注意：分割得到的每个字符串都必须是平衡字符串，且分割得到的平衡字符串是原平衡字符串的连续子串。

返回可以通过分割得到的平衡字符串的 最大数量 。


# 解答

```C++

class Solution {
public:
    int balancedStringSplit(string s) {
        int ans = 0;
        int cur = 0;
        for(char ch : s){
            if(ch == 'L') {
                cur++;
            } else {
                cur--;
            }
            if(cur == 0) {
                ans++;
            }
        }
        return ans;
    }
};

```

