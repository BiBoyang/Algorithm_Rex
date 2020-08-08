# LeetCode_0205 同构字符串
给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

示例 1:
```
输入: s = "egg", t = "add"
输出: true
```
示例 2:
```
输入: s = "foo", t = "bar"
输出: false
```
示例 3:
```
输入: s = "paper", t = "title"
输出: true
```

**说明:**
```
你可以假设 s 和 t 具有相同的长度。
```

# 解答
```C++
class Solution {
public:
    bool helper(string a,string b) {
        unordered_map<char,char> map;
        for(int i = 0;i<a.size();i++) {
            char c1 = a[i];
            char c2 = b[i];
            if(map.count(c1) > 0) {
                if(map[c1] != c2) {
                    return false;
                }
            } else {
                map.insert(make_pair(c1,c2));
            }
        }
        return true;
    }
    bool isIsomorphic(string s, string t) {
        return helper(s, t) && helper(t, s);
    }
};
```

* 时间复杂度：O(n)。n 是字符串的长度。
* 空间复杂度：O(n)。n 是字符串的长度。