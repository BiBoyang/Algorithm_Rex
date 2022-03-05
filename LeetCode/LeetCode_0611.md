# LeetCode_0611. 有效三角形的个数


给定一个包含非负整数的数组 nums ，返回其中可以组成三角形三条边的三元组个数。

 
示例 1:

```
输入: nums = [2,2,3,4]
输出: 3
解释:有效的组合是: 
2,3,4 (使用第一个 2)
2,3,4 (使用第二个 2)
2,2,3
```

示例 2:

```
输入: nums = [4,2,3,4]
输出: 4
```

提示:

* 1 <= nums.length <= 1000
* 0 <= nums[i] <= 1000


# 解答

```C++
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        int len = nums.size();
        sort(nums.begin(), nums.end());
        int ans = 0;
        for (int i = 0; i < len; i++) {
            int k = i;
            for (int j = i + 1; j < len; j++) {
                while (k + 1 < len && nums[k + 1] < nums[i] + nums[j]) {
                    ++k;
                }
                ans += max(k - j, 0);
            }
        }
        return ans;
    }
};
```

* 时间复杂度：O(n^2)，其中 n 是数组 nums 的长度。我们需要O(nlogn) 的时间对数组 nums 进行排序，随后需要 O(n^2)的时间使用一重循环枚举 a 的下标以及使用双指针维护 b,c 的下标。
* 空间复杂度：O(logn)，即为排序需要的栈空间。

