# LeetCode_0424 替换后的最长重复字符
给你一个仅由大写英文字母组成的字符串，你可以将任意位置上的字符替换成另外的字符，总共可最多替换 k 次。在执行上述操作后，找到包含重复字母的最长子串的长度。

**注意:**

字符串长度 和 k 不会超过 104。

示例 1:
```
输入:
s = "ABAB", k = 2

输出:

解释:
用两个'A'替换为两个'B',反之亦然。
```

示例 2:
```
输入:
s = "AABABBA", k = 1

输出:
4

解释:
将中间的一个'A'替换为'B',字符串变为 "AABBBBA"。
子串 "BBBB" 有最长重复字母, 答案为 4。
```

# 解答
使用滑动窗口的方法。


```C++
class Solution {
public:
    int characterReplacement(string s, int k) {
        unordered_map<char,int> map;
        int left = 0,right = 0,result = 0,maxCount = 0;
        while(right < s.size()) {
            map[s[right] - 'A']++;
            maxCount = max(maxCount,map[s[right]-'A']);
            if(right - left + 1 - maxCount > k) {
                map[s[left] - 'A']--;
                left++;
            }
            result = max(result,right - left + 1);
            right++;
        }
        return result;
    }
};
```

* 时间复杂度：O(n)。n 为字符串长度
* 空间复杂度：O(1)。创建一个哈希表，字符最多26个。
