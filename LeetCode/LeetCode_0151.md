# LeetCode_151. 翻转字符串里的单词


给定一个字符串，逐个翻转字符串中的每个单词。

说明：

无空格字符构成一个 单词 。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

示例 1：
```
输入："the sky is blue"
输出："blue is sky the"
```

# 解答

```C++
class Solution {
public:
    string reverseWords(string &s) {
       int size = s.size();
        if(size <= 0){
            return "";
        }//if
        // 前导0
        int index = 0;
        while(s[index] == ' '){
            ++index;
        }//while
        int left = index;
        // 后导0
        index = size - 1;
        while(s[index] == ' '){
            --index;
        }//while
        int right = index;
        // 连续空格只保留一个
        for(int i = left;i <= right;){
            if(i > left && s[i-1] == ' ' && s[i] == ' '){
                s.erase(i-1,1);
                --right;
            }//if
            else{
                ++i;
            }
        }//for
        // 翻转
        int start = left,end = left;
        for(int i = left;i <= right+1;++i){
            if(i == right+1 || s[i] == ' '){
                Reverse(s,start,end-1);
                ++end;
                start = end;
            }//if
            else{
                ++end;
            }//else
        }//for
        // 整体翻转
        Reverse(s,left,right);
        s = s.substr(left,right - left + 1);
        return s;
    }
private:
    void Reverse(string&s, int left, int right) {
        while(left < right) {
            char ch = s[right];
            s[right--] = s[left];
            s[left++] = ch;
        }        
    }
};
```