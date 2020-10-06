# LeetCode_0093. 复原IP地址

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效的 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效的 IP 地址。

 

示例 1：
```
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
```
示例 2：
```
输入：s = "0000"
输出：["0.0.0.0"]
```
示例 3：
```
输入：s = "1111"
输出：["1.1.1.1"]
```
示例 4：
```
输入：s = "010010"
输出：["0.10.0.10","0.100.1.0"]
```
示例 5：
```
输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
 ```

提示：

* 0 <= s.length <= 3000
* s 仅由数字组成

# 解答

```C++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> res;
        helper(s, 0, "", res);
        return res;
    }
    void helper(string s, int n, string out, vector<string>& res) {
        if (n == 4) {
            if (s.empty()) 
                res.push_back(out);
        } else {
            for (int k = 1; k < 4; ++k) {
                if (s.size() < k) break;
                int val = atoi(s.substr(0, k).c_str());
                if (val > 255 || k != to_string(val).size()) 
                    continue;
                helper(s.substr(k), n + 1, out + s.substr(0, k) + (n == 3 ? "" : "."), res);
            }
        }
    }
};
```