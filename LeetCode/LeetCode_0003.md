# LeetCode_0003 无重复字符最长子串
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

> * 示例 1:       
输入: "abcabcbb"      
输出: 3       
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。       

> * 示例 2:       
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

> * 示例 3:
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

# 解答

## 方法一：hash法

直接把字符加入hash表，然后判断。
时间复杂度：O(n^3) 。

空间复杂度：O(min(n,m))，我们需要 O(k)的空间来检查子字符串中是否有重复字符，其中 k 表示 Set 的大小。而 Set 的大小取决于字符串 n 的大小以及字符集/字母 m 的大小。

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //最长字符串长度
        int maxLength = 0;
        unordered_map<char,int>hashMap;
        //临时字符串长度
        int len = 0;
        for(int i = 0;i < s.size();i++) {
            if(hashMap.count(s[i]) == 0) {
                len += 1;
                hashMap[s[i]] = i;
            } else {
                len = 0;
                i = hashMap[s[i]];
                hashMap.clear();
            }
            if(maxLength < len)
                maxLength = len;   
        }     
        return maxLength;
    }
};
```
## 方法二

上一个方法有着明显的问题，我们要对hash表做多次操作。我们可不可以优化一下呢？
可以的。
注意点
> * ``left = max(left, hashMap[s[right]]);``，这里要注意，这里因为是在循环内第一行，所以我们要明白，这里的hashMap[s[right]]使用的实际上是上一轮的值，如果这里有值了，说明已经存在相同的字符了，至少是第二轮

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //使用hash
        unordered_map<char,int> hashMap;
        int maxLength = 0;
        int left = 0;//每个无重复字符串的起始
        for(int right = 0;right<s.size();right++) {
            left = max(left, hashMap[s[right]]);
            hashMap[s[right]] = right + 1;
            maxLength = max(maxLength,right - left + 1);
        }
        return maxLength;
    }
};
```
## 方法三
记录上一个点的方法。
我们创建一个字符串 **abcd1bc**.

| i  | 前Last [i] | left | 后Last[i] |
| --- | --- | --- | --- |
| 0 | -1 | 0 | 0 |
| 1 | -1 | 0 | 1 |
| 2 | -1 | 0 | 2 |
| 3 | -1 | 0 | 3 |
| 4 | 0 | 1 | 4 |
| 5 | 1 | 2 | 5 |
| 6 | 2 | 3 | 6 |

> 1. 开始遍历字符串;

> 2. 如果没有遇到重复字母，我们可以把**maxLen**每次都加1;

> 3. 没有遇到重复字符的时候，对应的字符的**last[s[i]]**都会为-1，但是会保存当前**i**，以便在下次遇到的时候用到;

> 4. 当我们遇到重复字符的时候，**last[s[i]]**说明不是-1了，则会大于等于left；

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int maxlen = 0;
        int left = 0;//不重复最左有效位置
        int last[255];//记录每个字母上一次出现的位置
        memset(last,-1,sizeof(last));
        for(int i = 0;i < s.size();i ++) {
            //当字符串遇到相同的字符的时候，序号为上一个字符位置+1；记录重复字符的总量
            if(last[s[i]] >= left) 
                left = last[s[i]] + 1;
            last[s[i]] = i;
            maxlen = max(maxlen,i - left + 1);
        }
        return maxlen;
    }
};
```
或者
```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int maxlen = 0;
        int left = -1;//不重复最左有效位置
        int last[255];//记录每个字母上一次出现的位置
        memset(last,-1,sizeof(last));
        for(int i = 0;i < s.size();i ++) {
            left = max(left,last[s[i]]);
            last[s[i]] = i;
            maxlen = max(maxlen,i - left);
        }
        return maxlen;
    }
};
```