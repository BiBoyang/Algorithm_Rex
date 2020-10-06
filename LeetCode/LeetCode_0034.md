# LeetCode_0034 在排序数组中查找元素的第一个和最后一个位置

* 二分查找

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```
示例 2:
```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

# 解答

```C++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {

    if(nums.size() == 0)
		return vector<int>({-1, -1});
	int n = nums.size();
	int b, e;
	int l = 0, r = n;
	while(l < r){
		int m = l + (r - l) / 2;
		if(nums[m]< target)
			l = m + 1;
		else
			r = m;
	}
	b = l;
	if(b == n || nums[b] != target)
		return vector<int>({-1, -1});
	l = 0, r = n;
	while(l < r){
		int m = l + (r - l) / 2;
		if(nums[m] <= target)
			l = m + 1;
		else
			r = m;
	}
	e = l;
	return vector<int>({b, e - 1});
    }    
};
```