# LeetCode_1119 删除字符串中的元音
给你一个字符串 S，请你删去其中的所有元音字母（ 'a'，'e'，'i'，'o'，'u'），并返回这个新字符串。

示例 1：

> 输入："leetcodeisacommunityforcoders"
> 输出："ltcdscmmntyfrcdrs"

示例 2：

> 输入："aeiou"
> 输出：""

 

提示：
>   S 仅由小写英文字母组成。
>   1 <= S.length <= 1000

# 解答
```C++
class Solution {
public:
    string removeVowels(string S) {
        string res="";
        for(auto c:S) {
            if(c!='a' && c!='e' && c!='i' && c!='o' && c!='u') {
                res+=c;
            }
        }
        return res;
    }
};

```