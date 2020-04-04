# 面试题10- I. 斐波那契数列
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。


# 解答
## 方法一
```C++
class Solution {
public:
    int fib(int n) {
        if(n < 2) return n;
        int fibOne = 0,fibTwo = 1,res = 0;
        for(int i = 2;i <= n;i++) {
            res = fibOne + fibTwo;
            fibOne = fibTwo;
            fibTwo = res;
        }
        return res;
    }
};
```

## 方法二
```C++
class Solution {
public:
    int fib(int n) {
        if(n < 2) return n;
        return fib(n-1) + fib(n-2);
    }
};
```