
# LeetCode_0014 最长公共前缀
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"

示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。

说明:

所有输入只包含小写字母 a-z 。
## 解答
#### 方法一
可以采用纵向扫描或横向扫描
纵向扫描，就从位置0开始，对每一个位置比较所有的字符串，直到遇到不匹配的字符为止。
```C++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty())
            return "";
        for(int i= 0;i< strs[0].size();i++) {
            for(int j = 1;j < strs.size();j++) {
                if(strs[j][i] != strs[0][i])
                    return strs[0].substr(0,i);
            }
        }
        return strs[0];
    }
};
```

#### 方法二
方法二和方法一 的思路是一样的，不过我们可以做一些优化。
方法一遍历的时候，是将第一个字符串整个遍历了之后又继续遍历下去的，我们可以思考一下，假设第一个字符串很长，那么我们将要遍历的时间就会过长。
那么，我们可以优化一下思路，在遍历的第一个字符串的时候先对标注每一个字符，如果后续的单词字符和它不匹配了，也就没有必要继续下去了。

时间复杂度：O(S)，S 是所有字符串中字符数量的总和。

最坏情况下，输入数据为 n 个长度为 m 的相同字符串，算法会进行 S = m * n 次比较。可以看到最坏情况下，本算法的效率与算法一相同，但是最好的情况下，算法只需要进行 n∗minLen 次比较，其中 minLen 是数组中最短字符串的长度。


```C++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty())
            return "";
        for(int i= 0;i< strs[0].size();++i) {
            //找到第一个单词的第i个字符
            char temp = strs[0][i];
            for(int j = 1;j<strs.size();j++) {
                /*
                * 注意i是第一个字符的下标，我们要记住它实际上实际上计算size的时候少1的
                * 前一个是假定第一个单词就是短的单词，后续的单词只需要计算前i个单词
                * 后一个是判断单词不相同
                */
                if(i == strs[j].size() || strs[j][i] != temp) {
                    return strs[0].substr(0,i);
                }
            }            
        }
        return strs[0];
    }
};
```



