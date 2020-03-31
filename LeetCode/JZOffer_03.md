# 剑指Offer_03 数组中重复的数字
找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：
```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```
# 解答
## 方法一
直接使用hashMap。
```C++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
	    unordered_map<int, int> hashmap = {};   
        for(int i=0;i<nums.size();i++) {
            if(hashmap[nums[i]] == 0) {
                hashmap[nums[i]]++;
            }else{
                return nums[i];
            }
        }   
        return 0;
    }
};
```
时间复杂度：O(n)。
空间复杂度：O(1)。

## 方法二
如果当前数字和当前下表不一样，我们就把他们交换。
```C++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        for(int i = 0;i<nums.size();i++) {
            while(i != nums[i]) {
                if(nums[i] == nums[nums[i]]){
                    return nums[i];
                } else {
                    swap(nums[i], nums[nums[i]]);
                }
            }
        }
        return 0;
    }
};
```
