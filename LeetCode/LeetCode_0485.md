# LeetCode_485 最大连续1的个数
给定一个二进制数组， 计算其中最大连续1的个数。

示例 1:

> 输入: [1,1,0,1,1,1]
> 输出: 3
> 解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.

注意：
```
    输入的数组只包含 0 和1。
    输入数组的长度是正整数，且不超过 10,000。
```

# 答案
创建两个数。一个用于记录最大总长度，一个用于记录每个连续的长度
```
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int MaxOne = 0;
        int One = 0;
        for(auto num : nums) {           			
            if(num == 1) 
				One++;
            else
                One = 0;
            MaxOne = max(MaxOne,One);
        }
        return MaxOne;
    }
};
```