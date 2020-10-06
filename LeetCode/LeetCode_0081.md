# LeetCode_0081 搜索旋转排序数组II

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

示例 1:
```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```
示例 2:
```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```
进阶:
* 这是 搜索旋转排序数组 的延伸题目，本题中的 nums  可能包含重复元素。
* 这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？

# 解答

```C++
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        if (nums.empty())
            return false;
        return binSearch(nums,0,nums.size() - 1,target);
    }
    //用递归的方式
private:
    bool binSearch(vector<int> &nums,int left,int right,int target) {
        //去除干扰
        while(nums[left] == nums[right] && left < right)
            left++;
        if(left == right && nums[left] != target )
            return false;
        int mid =  left + ((right - left) / 2);
        if(nums[mid] == target || nums[left] == target || nums[right] == target)
            return true;
        
        if(nums[left] < nums[right]) {
            if(nums[mid] < target)
                return binSearch(nums,mid + 1,right,target);
            else 
                return binSearch(nums,left,mid,target);
        } else {
            if (nums[mid] >= nums[left]) {      
                if (target < nums[mid] && target > nums[left]) 
                    return binSearch(nums, left, mid, target); 
                else 
                    return binSearch(nums, mid + 1, right, target); 
            } else { 
                if (target > nums[mid] && target < nums[right]) 
                    return binSearch(nums, mid+1, right, target); 
                else 
                    return binSearch(nums, left, mid, target); }
        } 
        return false;

    }
};
```