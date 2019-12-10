# LeetCode_0067 二进制求和
给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 1 和 0。

> * **示例 1:**       
输入: a = "11", b = "1"       
输出: "100"

> * **示例 2:**     
输入: a = "1010", b = "1011"
输出: "10101"

# 解答
已知得到的是两个字符串，这样我们可以比较简单的两个都是“1”就进1.
这个时候，为了避免我们会遇到长度不够的情况，我们需要把两个字符串补充到一样齐：方法就是在短的那个字符串前面加 `0`；然后我们又后往前遍历字符串，将每个位置的


```C++

#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    string addBinary(string a,string b) {
        int lenA = a.size();
        int lenB = b.size();
        while (lenA < lenB) {
            a = a + '0';
            lenA++;
        }
        while (lenA > lenB) {
            b = b + '0';
            lenB++;
        }
        for (int i = lenA - 1; i > 0; i--) {
            a[i] = a[i] - '0' + b[i];
            if(a[i] >=  '2') {
                a[i] = (a[i] - '0') % 2 + '0';
                a[i-1] = a[i-1] + 1;
            }
        }
        a[0] = a[0] - '0' + b[0];
        if(a[0] >= '2') {
            a[0] = (a[0] - '0') % 2 + '0';
            a = '1' + a;
        }
        return a;
    }
};
-----------------------------------------
-----------------------------------------
void UnitTest(string a,string b) {
    Solution sol;
    string str1 = a;
    string str2 = b;
    string res = sol.addBinary(str1, str2);
    cout << "答案：" << a<<endl;
}

int main(int argc, const char * argv[]) {
    // insert code here...
    std::cout << "Hello, World!\n";
    
    string str1("0");
    string str2("0");
    
    UnitTest(str1, str2);
    
    return 0;
}
```