# LeetCode_387 字符串中的第一个唯一字符
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

案例:

s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.

 

注意事项：您可以假定该字符串只包含小写字母。
## 解答
```
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char,int> hashMap;
        for(int i = 0;i< s.size();i++) {
            hashMap[s[i]] += 1;
        }
        for(int i = 0;i< s.size();i++) {
            if(hashMap[s[i]] == 1){
                return i;
            }
        }
        return -1;
    }
};
```