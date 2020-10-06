# LeetCode_1118 一月有多少天
指定年份 Y 和月份 M，请你帮忙计算出该月一共有多少天。

## 解答
```C++
class Solution {
public:
    int numberOfDays(int Y, int M) {
        int days[12] = {31,28,31,30,31,30,31,31,30,31,30,31};
        int res = days[M - 1];
        if(((Y % 4 == 0 && Y % 100 != 0) || (Y % 400 == 0)) && M == 2) return res + 1;
        return res;
    }
};
```