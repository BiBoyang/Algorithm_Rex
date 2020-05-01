# 字符串解压缩

有一种简易压缩算法：针对由全部小写字母组成的字符串，将其中连续超过两个相同字目的部分压缩成连续个数加该字母，其他部分保持原样不变。

例如，字符串：aaabccccd 经过压缩成为字符串：3ab4cd。请您编写一个unZip函数，根据输入的字符串，判断其是否为合法压缩过的字符串。
若输入合法，则输出解压后的字符串，否则输出：!error 来报告错误。

测试：3ab4cd合法，aa4b合法,caa4b合法,3aa4b不合法,22aa不合法,2a4b不合法,22a合法


# 解答
这道题很简单，直接暴力从头到尾捋一遍即可。

环境：Xcode

```C++
#include <iostream>
#include <string.h>

using namespace std;

void unZip(string inPut) {
    int len = (int)inPut.length();
    if(len == 0) return;
    
    int inPutNum = 0;
    string outPutString = "";
    
    for(int i = 0;i<len;i++) {
        if(inPut[i] - '0' >= 0 && inPut[i] - '0' <= 9) {
            inPutNum = inPutNum * 10 + inPut[i] - '0';
            
        } else if(inPut[i] >= 'a' && inPut[i] <= 'z') {
            if(inPutNum > 0) {
                if(inPut[i] == inPut[i+1]) {
                    cout << "!Error" << endl;
                    return;
                }
                    
                for(int j = 0;j < inPutNum;j++) {
                    outPutString += inPut[i];
                }
                inPutNum = 0;
            } else {
                //三个字符重复
                if(inPut[i] == inPut[i+1]) {
                    
                    if(inPut[i+1] == inPut[i+2]) {
                        cout << "!Error" << endl;
                        return;
                    }
                }
                outPutString += inPut[i];
            }
        }
    }
    
    cout << "" << outPutString<< endl;
}


int main(int argc, const char * argv[]) {
    // insert code here...
    
    string str1 = "10ab4cdd";
    string str2 = "3abb4cd";
    string str3 = "3@bb4cd";
    string str4 = "3abbb4cd";
    string str5 = "1abb4cd";

    unZip(str1);
    unZip(str2);
    unZip(str3);
    unZip(str4);
    unZip(str5);
    
    return 0;
}
```