# LeetCode_0159 至多包含两个不同字符的最长子串

给定一个字符串 s ，找出 至多 包含两个不同字符的最长子串 t ，并返回该子串的长度。

示例 1:
```
输入: "eceba"
输出: 3
解释: t 是 "ece"，长度为3。
```
示例 2:
```
输入: "ccaabbb"
输出: 5
解释: t 是 "aabbb"，长度为5。
```

# 解答

```C++


class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
        if(s.size() < 3) return s.size();
        unordered_map<char,int> map;
        int left = 0,right = 0,res = 2;
        for(;right < s.size();right++) {
            map[s[right]]++;
            while(map.size() > 2) {
                map[s[left]]--;
                if(map[s[left]] == 0) {
                    map.erase(s[left]);
                }
                left++;
            }
            res = max(res, right - left + 1);
        }
        return res;
    }
};
```
* 时间复杂度：O(n)。n 是字符串 s 的长度。
* 空间复杂度：O(n)。