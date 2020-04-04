# 剑指Offer 5 ：替换空格
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."

# 解答

```C++
class Solution {
public:
    string replaceSpace(string s) {
        string res;
        for(auto &n:s) {
            if( n == ' ') {
                res.push_back('%');
                res.push_back('2');
                res.push_back('0');
            } else {
                res.push_back(n);
            }
        }
        return res;
    }
};
```

时间复杂度：O(n)
空间复杂度：O(n)