# LeetCode_1556 千位分隔数

给你一个整数 n，请你每隔三位添加点（即 "." 符号）作为千位分隔符，并将结果以字符串格式返回。

 

示例 1：
```
输入：n = 987
输出："987"
```
示例 2：
```
输入：n = 1234
输出："1.234"
```
示例 3：
```
输入：n = 123456789
输出："123.456.789"
```
示例 4：
```
输入：n = 0
输出："0"
```

提示：
* 0 <= n < 2^31

# 解答

```C++
class Solution {
public:
    string thousandSeparator(int n) {
        string s = to_string(n % 10);
        int digits = 1;
        n /= 10;
        while (n) {
            if (digits % 3 == 0) {
                s = "." + s;
            }
            s = to_string(n % 10) + s;
            n /= 10;
            digits++;
        }
        return s;
    }
};
```