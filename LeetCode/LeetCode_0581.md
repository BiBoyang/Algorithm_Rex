# LeetCode_0581. 最短无序连续子数组

给你一个整数数组 nums ，你需要找出一个 连续子数组 ，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

请你找出符合题意的 最短 子数组，并输出它的长度。

 

示例 1：
```
输入：nums = [2,6,4,8,10,9,15]
输出：5
解释：你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```

示例 2：
```
输入：nums = [1,2,3,4]
输出：0
```

示例 3：
```
输入：nums = [1]
输出：0
```

# 解答

用 left、right来记录最短无序数组的左右边界。

```C++

class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int len = nums.size();
        int maxN = INT_MIN;
        int minN = INT_MAX;
        int left, right = -1;
        for(int i = 0;i < len;i++){
            if(maxN > nums[i]){
                right = i;
            } else {
                maxN = nums[i];
            }
            if(minN < nums[len - i - 1]) {
                left = len - 1 - i;
            } else {
                minN = nums[len - i -1];
            }
        }
        if(right == -1){
            return 0;
        } else {
            return right - left + 1;
        }
    }
};
```

* 时间复杂度：O(n)。
* 空间复杂度：O(1)。