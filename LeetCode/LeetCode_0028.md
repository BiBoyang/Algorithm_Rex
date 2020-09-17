# LeetCode_0028. 实现 strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。


# 解答
## 方法一：双循环暴力搜索
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




## 方法三
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int lenh = haystack.size();
        int lenn = needle.size();
        
        if(lenn == 0) return 0;
        if(lenh == 0 || lenh < lenn) return -1;
        int i = 0;
        
        while(i < (lenh - lenn + 1)) {
            int c = 0, l = 0, rev = false;
            for(int j = 0;j < lenn;j++) {
                if(j>0 && haystack[i+j] == needle[0] && l<1) {
                        rev = true;
                        c = j;
                        l++;
                }

                if(haystack[i+j] == needle[j]){
                    if(j == lenn-1) {
                        return i;
                    }
                } else {
                    if(j == 0) {
                        i++;
                        break;
                    } else if(rev) {
                        i += c;
                        break;
                    }
                i += j;
                break;
                }
            }
        }
        return -1;
    }
};
```