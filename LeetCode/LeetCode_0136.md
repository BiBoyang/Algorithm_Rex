# LeetCode_0136 只出现一次的数字
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```

# 解答
这里要运用到位运算的知识，
1. 任何数和 0 做异或运算，结果仍然是原来的数，即 a⊕0=a
2. 任何数和其自身做异或运算，结果是 000，即 a⊕a=0a 。
3. 异或运算满足交换律和结合律，即 a⊕b⊕a=b⊕a⊕a=b⊕(a⊕a)=b⊕0=b；


```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for(int i = 0;i<nums.size();i++) {
            res ^= nums[i];
        }
        return res;
    }
};
```