# LeetCode_567 字符串的排列
给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的子串。

示例1:

输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").

 

示例2:

输入: s1= "ab" s2 = "eidboaoo"
输出: False

 

注意：

> 输入的字符串只包含小写字母
> 两个字符串的长度都在 [1, 10,000] 之间

## 解答
#### 方法一
统计s1中字符出现的次数，不一样的是我们用一个变量cnt来表示还需要匹配的s1中的字符的个数，初始化为s1的长度，然后遍历s2中的字符，如果该字符在哈希表中存在，说明匹配上了，cnt自减1，哈希表中的次数也应该自减1，然后如果cnt减为0了，说明s1的字符都匹配上了，如果此时窗口的大小正好为s1的长度，那么说明找到了s1的全排列，返回true，否则说明窗口过大，里面有一些非s1中的字符，我们将左边界右移，同时将移除的字符串在哈希表中的次数自增1，如果增加后的次数大于0了，说明该字符是s1中的字符，我们将其移除了，那么cnt就要自增1
```
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        int n1 = s1.size(), n2 = s2.size(), cnt = n1, left = 0;      
        unordered_map<char,int>map;
        for(int i = 0;i< s1.size();i++) {
            map[s1[i]] ++;
        }
        for (int right = 0; right < n2; ++right) {
            if (map[s2[right]]-- > 0) 
                --cnt;
            while (cnt == 0) {
                if (right - left + 1 == n1)
                    return true;
                if (++map[s2[left++]] > 0) 
                    ++cnt;
            }
        }
        return false;
    }
};
```
#### 方法二
利用一个哈希表加上双指针，我们还是先统计s1中字符的出现次数，然后遍历s2中的字符，对于每个遍历到的字符，我们在哈希表中对应的字符次数减1，如果次数次数小于0了，说明该字符在s1中不曾出现，或是出现的次数超过了s1中的对应的字符出现次数，那么我们此时移动滑动窗口的左边界，对于移除的字符串，哈希表中对应的次数要加1，如果此时次数不为0，说明该字符不在s1中，继续向右移，直到更新后的次数为0停止，此时到达的字符是在s1中的。如果次数大于等于0了，我们看此时窗口大小是否为s1的长度，若二者相等，由于此时窗口中的字符都是在s1中存在的字符，而且对应的次数都为0了，说明窗口中的字符串和s1互为全排列，返回true.

```
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        int n1 = s1.size(), n2 = s2.size(), left = 0;
        unordered_map<char,int>map;
        for(int i = 0;i< s1.size();i++) {
            map[s1[i]] ++;
        }
        for (int right = 0; right < n2; ++right) {
            if (--map[s2[right]] < 0) {
                while (++map[s2[left++]] != 0) {
                }
            } else if (right - left + 1 == n1) 
                return true;
        }
        return n1 == 0;
    }
};
```

