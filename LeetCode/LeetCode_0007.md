
# LeetCode_0007 整数反转


给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例 1:

输入: 123
输出: 321

 示例 2:

输入: -123
输出: -321

示例 3:

输入: 120
输出: 21

注意:

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。



## 解答

方法：弹出和推入数字 & 溢出前进行检查

思路

我们可以一次构建反转整数的一位数字。在这样做的时候，我们可以预先检查向原整数附加另一位数字是否会导致溢出。

算法

反转整数的方法可以与反转字符串进行类比。

我们想重复“弹出” x 的最后一位数字，并将它“推入”到 rev 的后面。最后，rev 将与 x 相反。

要在没有辅助堆栈 / 数组的帮助下 “弹出” 和 “推入” 数字，我们可以使用数学方法。
```
//pop operation:
pop = x % 10;
x /= 10;

//push operation:
temp = rev * 10 + pop;
rev = temp;
```
但是，这种方法很危险，因为当 **temp=rev⋅10+pop**时会导致溢出。

幸运的是，事先检查这个语句是否会导致溢出很容易。

为了便于解释，我们假设 rev 是正数。

> 1. 如果 temp=rev⋅10+pop导致溢出，那么一定有 rev≥INT_MAX/10。
> 2. 如果 rev>INT_MAX/10，那么 temp=rev⋅10+pop一定会溢出。
> 3. 如果 rev==INT_MAX/10​，那么只要 pop>7，temp=rev⋅10+pop 就会溢出。

当 rev 为负时可以应用类似的逻辑。

```C++
class Solution {
public:
    int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > INT_MAX/10 || (rev == INT_MAX / 10 && pop > 7)) 
                return 0;
            if (rev < INT_MIN/10 || (rev == INT_MIN / 10 && pop < -8)) 
                return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
};
```