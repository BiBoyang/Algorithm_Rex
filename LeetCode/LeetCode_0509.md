# LeetCode_0509 斐波那契数
斐波那契数，通常用 F(n) 表示，形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.

给定 N，计算 F(N)。

## 题解
经典题，不多说了。
#### 方法一：递归
```C++
class Solution {
public:
    int fib(int N) {
        if(N == 0) {
            return 0;
        } else if(N == 1) {
            return 1;
        } else {
            return fib(N - 1) + fib(N - 2);
        } 
    }
};
```
#### 方法二：动态规划
```C++
class Solution {
public:
    int fib(int N) {
        if(N < 2) return N;
        int fibOne = 0,fibTwo = 1,res = 0;
        for(int i = 2;i <= N;i++) {
            res = fibOne + fibTwo;
            fibOne = fibTwo;
            fibTwo = res;
        }
        return res;
    }
};
```