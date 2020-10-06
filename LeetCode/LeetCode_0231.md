# LeetCode_231 2的幂
给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

示例 1:

输入: 1
输出: true
解释: 20 = 1

示例 2:

输入: 16
输出: true
解释: 24 = 16

示例 3:

输入: 218
输出: false

## 解答

## 方法一
暴力法
```
class Solution {
public:
    bool isPowerOfTwo(int n) {
        int res;
        if(n == 1) 
            return true;
        if(n <= 0) 
            return false;
        while(n != 1) {
            res = n % 2;
            if(res != 0) return false;
            n = n/2;
        }
        return true; 
    }
};
```

## 方法二
4的二进制是100，只要是2的倍数，二进制最高位是1，其余是0。4-1的二进制是011，可以看见，刚好所有的位置01对换。4和3相与，就是0。
&操作，相同位的两个数字都为1，则为1；若有一个不为1，则为0
因此n & n-1为0，说明它就是2的倍数
```
class Solution {
public:
    bool isPowerOfTwo(int n) {

    if(n<=0) 
        return false; 
        if((n&n-1)==0) 
            return true; 
        else 
            return false;   
    }
};
```


