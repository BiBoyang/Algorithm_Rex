# LeetCode_0003 无重复字符的最长子串

给定一个字符串 s ，请你找出其中不含有重复字符的 最长 子串 的长度。

# 解答

看到“出不含重复字符”第一时间想到了 hash 表。

```Cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //char 记录字符，int 记录重复字符出现的下一个位置
        unordered_map<char,int> hashs;
        int maxLength = 0;
        int left = 0;

        for(int right = 0;right < s.size();right++){
            //这里会对 hashs[s[right]] 字符进行第一次赋值，默认为 0
            left = max(left,hashs[s[right]]);
            //hashs 记录的是重复的字符的下一个索引，不是当前索引！再往后是没有重复的
            //因为记录的是重复字符的下一个索引，所以要+1
            hashs[s[right]] = right + 1;

            maxLength = max(maxLength, right - left + 1);
        }
        //abbbabcd
        return  maxLength;
    }
};
```

细解：

代码里有一个 unordered_map<char, int>，应该是用来存储字符最近出现的位置。然后有 maxLength 记录最长子串的长度，left指针作为窗口的左边界，right 指针遍历整个字符串。

这里利用了 unordered_map = hashMap[key] 的特点：

* 在 C++ 中，当通过 hashMap[key] 访问一个不存在的键时：
  ​​会自动插入该键​​，并将其值初始化为该类型的默认值（对 int 来说是 0）。所以 **left = max(left,hashs[s[right]]);** 这段代码里的 **hashs[s[right]]** 的值就是 0 。

接着在 **hashs[s[right]] = right + 1;** 中，hashMap 记录的是这个字符最靠右的那个，如果有更新，就会覆盖原来的值。

在循环里，对于每个 right，更新 left 的值。这里的 left 取的是当前 left 和 hashMap 中 s[right] 的值中的较大者。这一步是关键。比如，当遇到重复字符时，hashMap 中已经存了该字符之前的位置，所以 left 要跳到那个位置的下一个，

注意！是**之前位置**的下一个，而非当前索引！！！这里是最容易被误解的地方。

为什么要存“下一个索引”？​​

当发现重复字符时，窗口左边界 left 需要直接跳到​​重复字符上次出现位置的下一个索引​​，以确保窗口内无重复。

* 例如，字符串 "abba"：
  遍历到第二个 'b'（索引2）时，hashMap['b'] = 2（上一次出现位置是索引1，所以存的是 1 + 1 = 2）。
* left 会更新到 2，窗口变为 [2, 2]（即当前字符 'b'）。

最后，因为记录的 left 实际上是重复字符的下一个索引，所以做 right - left  的时候别忘记 +1 。

