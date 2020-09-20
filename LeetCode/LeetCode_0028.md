# LeetCode_0028. 实现 strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。


# 解答
## 方法一：双指针暴力搜索
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int len1 = haystack.size(), len2 = needle.size();
        for(int i = 0; i < len1 - len2 + 1; ++i){
            bool flag = true;
            for(int j = 0; j < len2; ++j){
                if(haystack[i+j] != needle[j]){
                    flag = false;
                    break;
                }
            }
            if(flag){
                return i;
            }
        }
        return -1;
    }

};
```
* 时间复杂度：最坏为 O((N-L)L)，最优为 O(L)。 N 为 haystack 字符串的长度，L 为 needle 字符串的长度
* 空间复杂度：O(1)。


## 方法二

KMP

```C++
class Solution {
public:
    vector<int> getNext(string str) {
        int len = str.size();
        vector<int> next;
        next.push_back(-1);
        int i = 0,j = -1;
        while(i < len){
            if( (j == -1) || str[i] == str[j]){
                i++;
                j++;
                next.push_back(j);
            } else {
                j = next[j];
            }
        }
        return next;
    }
        int strStr(string haystack, string needle) {
        if(needle.empty())
            return 0;
        
        int i=0;//源串
        int j=0;//子串
        int len1 = haystack.size();
        int len2 = needle.size();
        vector<int> next;
        next=getNext(needle);
        while((i<len1)&&(j<len2))
        {
            if((j==-1)||(haystack[i]==needle[j]))
            {
                i++;
                j++;
            }
            else
            {
                j=next[j];//获取下一次匹配的位置
            }
        }
        if(j==len2)
            return i-j;
        
        return -1;
    }
};
```


## 方法三
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.empty())
            return 0;
        
        int hayLen = haystack.size();
        int nedLen = needle.size();
        int i = 0,j = 0;
        int k = 0;
        int m = nedLen;//匹配时，文本串中参与匹配的元素的下一位
        
        for(;i<hayLen;) {
            if(haystack[i] == needle[j]) {
                if(j == nedLen - 1) return i-j;
                i++;
                j++;
            } else {
                for(k = nedLen - 1;k >= 0;k--) {
                    if(needle[k]==haystack[m]) break;
                }
                i = m-k;//i为下一次匹配源串开始首位 Sunday算法核心：最大限度跳过相同元素
                j = 0;
                m = i + nedLen;
                if(m > hayLen) return -1;
            }
        }
        return -1;
    }
};
```