# LeetCode_0724 寻找数组的中心索引
给定一个整数类型的数组 nums，请编写一个能够返回数组“中心索引”的方法。

我们是这样定义数组中心索引的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。

如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

## 解答
## 方法一
算出总量，然后对比

```
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int sum = 0, sumLeft = 0, sumRight = 0;
        for (auto n : nums){
            sum = sum + n;
        }
        for (int i= 0;i < nums.size();i++) {
            if (i==0) {
                sumLeft = 0;
            } else {
                sumLeft = sumLeft + nums[i-1];
            }
            sumRight = sum - sumLeft - nums[i];
            if (sumLeft==sumRight){
                return i;
            }
        }
        return -1;
    }
};
```