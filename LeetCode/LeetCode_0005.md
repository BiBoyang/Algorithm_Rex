
# LeetCode_0005 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

示例 2：

输入: "cbbd"
输出: "bb"


# 解答
## 方法一
动态规划。
设状态dp[j][i]表示索引j到索引i的子串是否是回文串。则转移方程为：
![](https://upload-images.jianshu.io/upload_images/6946981-a5f3dcc2b314fd49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/799)
我们利用这个去进行计算。
即：
从单一的回文，到两个回文、三个回文往上增长。
P(i,j)=(P(i+1,j−1) and Si​==Sj​)

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        if(s.empty()) return "";
        int len = s.size();
        if(len == 1) return s;    
        int longest = 1;
        int start = 0;
        vector<vector<int>> dp(len,vector<int>(len));
        for(int i = 0;i< len;i++) {
            dp[i][i] = 1;
            if(i<len-1) {
                if(s[i] == s[i+1]) {
                    dp[i][i+1] = 1;
                    start = i;
                    longest = 2;
                }   
            }
        }
        //子串长度,从三开始才有正确意义上的回文
        for (int l = 3; l <= len; l++) {
            //枚举子串的起始点
            for (int i = 0; i+l-1 < len; i++) {
                int j = l+i-1;//回文字符的终点下标
                if (s[i] == s[j] && dp[i+1][j-1]==1) {
                    dp[i][j] = 1;
                    start=i;
                    longest = l;
                }
            }
        }
        return s.substr(start,longest); 
    }
};
```
时间复杂度：O(n^2 )
空间复杂度：O(1)



## 方法二

Manacher 算法。
```C++
class Solution {
public:
	void HandleString(string &s) {
		if (s.empty())
		{
			return;
		}
        string temp = "$#";
		for (auto i : s) {
			temp += i;
			temp += '#';
		}
		s = temp;
    }
	void GetSouceString(string &s) {
		if (s.empty())
		{
			return;
		}
		string temp;
		for (int i = 1; i < s.size(); i += 2)
		{
			temp += s[i];
		}
		s = temp;
	}

	string longestPalindrome(string &s) {
        if(s.empty())
            return "";
		//添加#号
        HandleString(s);
        
		int size = s.size();
		int *len = new int[size]();
		pair<int, int> result{ 0,0 };//结果的起始下标和长度

		int center = 0;
		int rightside = 0;
		for (int i = 1; s[i] != '\0'; ++i) {
			len[i] = rightside > i ? min(len[2 * center - i], rightside - i) : 1;
			while (s[i + len[i]] == s[i - len[i]])
			{
				++len[i];
			}
			if (i + len[i] > rightside) {
				rightside = i + len[i];
				center = i;
			}
			if (result.second < len[i]) {
				result.first = i - len[i] + 1;
				result.second = len[i];
			}
		}
		string s2(s.begin() + result.first, s.begin() + result.first + result.second * 2 - 1);
        //变回来 
		GetSouceString(s2);
		return s2;
	}
};
```

