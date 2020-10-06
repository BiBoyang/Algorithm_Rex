# LeetCode_459 重复的子字符串
给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

示例 1:

输入: "abab"

输出: True

解释: 可由子字符串 "ab" 重复两次构成。

示例 2:

输入: "aba"

输出: False

示例 3:

输入: "abcabcabcabc"

输出: True

解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)

## 解答
暴力法。
```C++
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        //暴力方法，穷举所有能分段的程度去分段
        int strLen = s.size();
        for(int i = 2;i <= strLen;i++) {
            if (strLen % i == 0) {//剪枝，只有可以分均分成num端，才有分的意义 
                bool flag = true;
                int len = strLen / i;
                string tempStr = s.substr(0, len);//第一段 
                //截取后面的每一段，与第一段匹配 
                for (int index = len; index < strLen; index += len) { 
                    if (tempStr != s.substr(index, len)) {
                        //出现不同的段则停止 
                        flag = false; break;
                    } 
                }
                if (flag) {
                    //如果符合条件则返回 
                    return true;
                }
            }

        }
        return false;
    }
};
```