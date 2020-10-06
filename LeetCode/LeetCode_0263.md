# LeetCode_263 丑数（ugly number）
丑数就是只包含质因数 2, 3, 5 的正整数。

示例 1:

输入: 6
输出: true
解释: 6 = 2 × 3
示例 2:

输入: 8
输出: true
解释: 8 = 2 × 2 × 2
示例 3:

输入: 14
输出: false 
解释: 14 不是丑数，因为它包含了另外一个质因数 7。
说明：

> 1. 1 是丑数。
> 2. 输入不会超过 32 位有符号整数的范围: [−231,  231 − 1]。

## 解答
#### 方法一：暴力法
直接采用因数分解的方法去解决。一直往下分解，直到不能分解。如果结果为1，说明是丑数，否则不是。
```C++
class Solution {
public:
    bool isUgly(int num) {
        if(num == 0) {
            return false;
        } else if(num == 1) {
            return true;
        } else {
            while(num % 2 == 0) {
                num /= 2;
            }
            while(num % 3 == 0) {
                num /= 3;
            }
            while(num % 5 ==0) {
                num /= 5;
            }
            if(num == 1) {
                return true;
            } else {
                return false;
            }   
        }
    }
};

```

#### 方法二
上面的方法虽然简单，但是存在一个问题。那就是不管是不是丑数，都会进行一次判断。我们观察定义，可以发现，每一个丑数都是另外一个丑数的乘以2、3或者5的结果。
我们把得到的第一个丑数乘以2以后得到的大于M的结果记为M2。同样，我们把已有的每一个丑数乘以3和5，能得到第一个大于M的结果M3和M5。那么M后面的那一个丑数应该是M2,M3和M5当中的最小值：Min(M2,M3,M5)。比如将丑数数组中的数字按从小到大乘以2，直到得到第一个大于M的数为止，那么应该是2 * 2=4<M，3 * 2=6>M，所以M2=6。同理，M3=6，M5=10。所以下一个丑数应该是6。
```
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> ugly(n, 1), idx(3, 0);
        for (int i = 1; i < n; ++i){
            int a = ugly[idx[0]]*2, b = ugly[idx[1]]*3, c = ugly[idx[2]]*5;
            int next = min(a, min(b, c));
            if (next == a){
                ++idx[0];
            } 
            if (next == b){
                ++idx[1];
            } 
            if (next == c){
                ++idx[2];
            }
            ugly[i] = next;
        }
        return ugly.back();
    }
};

```