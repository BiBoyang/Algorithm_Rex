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
使用哈希表.
```C++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;  
        int sub=0;  //结果vector的下标值
        string tmp; //临时string
        unordered_map<string,int> work; //判断排序后单词是否存在，即字母组成是否一致
        for(auto str:strs)
        {
            tmp=str;
            sort(tmp.begin(),tmp.end());
            if(work.count(tmp))
            {
               res[work[tmp]].push_back(str);
            }
            else
            {
                vector<string> vec(1,str);
                res.push_back(vec);
                work[tmp]=sub++;
            }
        }
        return res;
    }
};

```