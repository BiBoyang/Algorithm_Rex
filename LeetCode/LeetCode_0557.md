# LeetCode_0557 反转字符串中的单词 III
给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

示例 1:

输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 

注意：在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

## 解答
最简单的暴力方法.
由后往前遍历字符串，遇到空格则翻转temp中的单词。

```C++
class Solution {
public:
    string reverseWords(string s) {
        string ans = ""; 
        string temp = ""; 
        int len = s.size();
        for(int i = 0; i <= len; ++ i) {
            if(s[i] == ' ' || s[i] =='\0') {
                reverse(temp.begin(),temp.end());
                ans += temp;
                ans += s[i]; 
                temp = ""; //初始化temp
            } else {
                temp += s[i]; 
            }
        }
        return ans;
    }
};
``` 


## 优化之后
上面的解法实际上有些过度了，我们可以换一种方式。
从前往后遍历字符串，然后将空格的时候，将之前的翻转。
```
#include <iostream>
#include <cstring>

using namespace std;

class Solution {
public:
    string reverseWords(string str) {
        str.append(" ");
        int begin = 0,end = 0;
        for (int i = 0; i < str.length(); i++) {
            if(str[i] == ' ') {
                end = i - 1;
                while (begin < end) {
                    swap(str[begin++], str[end--]);
                }
                begin = i + 1;
            }
        }
        str.pop_back();
        return str;
    }
};
//Unit Test
void test(string testStr) {
    Solution sol;
    string str = testStr;
    string ans = sol.reverseWords(str);
    cout << "UnitTest :" << ans << endl;
}

int main(int argc, const char * argv[]) {
    test("Let`s go !");// s`teL og !
    test("biboyang");//gnayobib
    test("Hello world");//olleH dlrow

    return 0;
}
```