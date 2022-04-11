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

首先对数组排序。
固定最长的一条边，运用双指针扫描
如果 nums[l] + nums[r] > nums[i]，同时说明 nums[l + 1] + nums[r] > nums[i], ..., nums[r - 1] + nums[r] > nums[i]，满足的条件的有 r - l 种，r 左移进入下一轮。
如果 nums[l] + nums[r] <= nums[i]，l 右移进入下一轮。
枚举结束后，总和就是答案。



```C++
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        int len = nums.size();
        int ans = 0;
        sort(nums.begin(),nums.end());

        for(int i = len - 1;i >= 2 ;i--) {
            int left = 0,right = i - 1;
            while(left < right) {
                if(nums[left] + nums[right] > nums[i]){
                    ans += right - left;
                    right--;
                } else {
                    left++;
                }
            }
        }
        return ans;
    }
};
```

* 时间复杂度：O(n^2)，其中 n 是数组 nums 的长度。我们需要O(nlogn) 的时间对数组 nums 进行排序，随后需要 O(n^2)的时间使用一重循环枚举 a 的下标以及使用双指针维护 b,c 的下标。
* 空间复杂度：O(logn)，即为排序需要的栈空间。

