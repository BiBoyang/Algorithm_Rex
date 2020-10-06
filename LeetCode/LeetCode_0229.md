# LeetCode_229 求众数 II
给定一个大小为 n 的数组，找出其中所有出现超过 ⌊ n/3 ⌋ 次的元素。

**说明:** 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

**示例 1**:

> 输入: [3,2,3]
> 输出: [3]

**示例 2**:

> 输入: [1,1,1,3,3,2,2,2]
> 输出: [1,2]

## 答案
修改一下摩尔法。
```
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
            vector<int> res;
    int x = 0, y = 0, cx = 0, cy = 0, count = 0;
    for (auto num : nums){
        if ((cx == 0 || num == x) && num != y){
            ++cx, x = num;
        } else if (cy == 0 || num == y){
            ++cy, y = num;
        } else {
            --cx, --cy;
        }
    }
    for (auto num : nums){
        if (x == num){
            ++count;
        }
    }
    if (count > nums.size()/3){
        res.push_back(x);
    }
    count = 0;
    for (auto num : nums){
        if (y == num){
            ++count;
        }
    }
    if (count > nums.size()/3 && x != y){
        res.push_back(y);
    }
    return res;
    }
};
```