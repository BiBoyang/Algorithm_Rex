# LeetCode_0049 字母异位词分组

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:
```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
说明：

* 所有输入均为小写字母。
* 不考虑答案输出的顺序。

# 解答
使用哈希表。

遍历字符串，然后将每个字符串排序。相同排序的放到一个桶子里。
```C++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> map;
        for(auto str: strs){
            string temp = str;
            sort(temp.begin(), temp.end());
            map[temp].push_back(str);
        }
        vector<vector<string>> ans;
        for(auto str: map){
            ans.push_back(str.second);
        }
        return ans;
    }
};
```
* 时间复杂度：O(NKlogK) 。N 是strs 的长度，K 是字符串最大的那个的长度。
* 空间复杂度：O(NK)。