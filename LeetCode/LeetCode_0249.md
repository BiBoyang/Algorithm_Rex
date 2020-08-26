# LeetCode_0249 移位字符串分组

给定一个字符串，对该字符串可以进行 “移位” 的操作，也就是将字符串中每个字母都变为其在字母表中后续的字母，比如：``"abc" -> "bcd"``。这样，我们可以持续进行 “移位” 操作，从而生成如下移位序列：

```
"abc" -> "bcd" -> ... -> "xyz"
```

给定一个包含仅小写字母字符串的列表，将该列表中所有满足 “移位” 操作规律的组合进行分组并返回。

 

示例：
```
输入：["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"]
输出：
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
解释：可以认为字母表首尾相接，所以 'z' 的后续为 'a'，所以 ["az","ba"] 也满足 “移位” 操作规律。
```

# 解答
这道题和 LeetCode_0049 字母异位词分组 其实非常类似，我们可以将所有的字符串，都转化为 a 开头的字符串，然后再将它们一同归类

```C++
class Solution {
public:
    vector<vector<string>> groupStrings(vector<string>& strings) {
        vector<vector<string>> res;
        unordered_map<string, vector<string>> hashmap;
        for(string s : strings){
            string str = s;
            for(int i = 0; i < str.size(); i++) {
                str[i] = (str[i] - s[0] + 26) % 26 +'a';
            }
            hashmap[str].push_back(s);
        }
        for(auto i : hashmap) {
            res.push_back(i.second);
        }
        return res;
    }
};
```