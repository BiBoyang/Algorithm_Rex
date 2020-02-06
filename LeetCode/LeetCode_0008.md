
# LeetCode_0008 字符串转换整数 (atoi)


请你来实现一个 atoi 函数，使其能将字符串转换成整数。

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

说明：

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231,  231 − 1]。如果数值超过这个范围，qing返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

示例 1:

输入: "42"
输出: 42

示例 2:

输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。

示例 3:

输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。

示例 4:

输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。

示例 5:



输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。

## 解答
题目比较简单，按顺序遍历即可。
从左往右遍历字符串，会有以下几种情况：
> 1. 如果遇到" "，直接continue；
> 2. 如果遇到“-”，标记为负数，以及下一位是数字，然后继续遍历；
> 3. 如果遇到“+”，标记为正数，以及下一位是数字，然后继续遍历；
> 4. 判断是否是数字，如果是数字，则直接中断退出循环；
> 5. 如果上面的都没有，则直接返回0。

然后从数字开始的地方进行遍历：
> 1. 先将字符转换为数字；
> 2. 判断当前字符是不是数字，如果不是，则直接返回res；
> 3. 判断res是否符合条件res > INT_MAX/10 || res*10 > INT_MAX-add，如果符合，则返回INT_MAX；
> 4. 判断res是否符合条件res < INT_MIN/10 || res*10 < INT_MIN+add，如果符合，则返回INT_MIN；
> 5. 然后通过判断正负，来进行计算。

```C++
class Solution {
public:
    int myAtoi(string str) {
        int res = 0;
        bool isNeg = false;//是否为负数
        if(str.size() == 0) {
            return res;
        }
        int left;
        bool nextMustBeNumber = false;
        for(left = 0;left < str.size();left++) {
            if(str[left] == ' ' && !nextMustBeNumber) {
                continue;
            } else if(str[left] == '-' && !nextMustBeNumber) {
                isNeg = true;
                nextMustBeNumber = true;
                continue;
            } else if( str[left] == '+' && !nextMustBeNumber ) {
                nextMustBeNumber = true;
                continue;
            } else if( isNum(str[left]) ) {
                break;
            } else {
                //这里直接返回零
                return res;
            }    
        }
        for( int i = left; i < str.size(); ++i  ) {
            //转换数字
            int add = str[i] - '0';
            //判断当前字符是不是数字
            if( add < 0 || add > 9 ) {
                return res;
            }
            if( !isNeg && (res > INT_MAX/10 || res*10 > INT_MAX-add) ) {
                return INT_MAX;
            } else if( isNeg && (res < INT_MIN/10 || res*10 < INT_MIN+add)) {
                return INT_MIN;
            }
            if(isNeg) {
                res = res*10 - add;
            }else{
                res = res*10 + add;
            }
        }
        return res;
    }

    bool isNum(char s) {
        int i = s - '0';
        if( i < 0 || i > 10 ) {
            return false;
        }
        return true;
    }
};

```

