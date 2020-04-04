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
        unordered_map<int,int> map;
        for(auto num:nums) {
            if(map[num] == 0) {
                map[num]++;
            } else {
                return num;
            }
        }
        return -1;
    }
};
```
或者
```
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int,int> hashMap;
        for(int i =0;i< nums.size();i++) {
            if(hashMap.count(nums[i]) != 0) {
                return nums[i];
            } else {
                hashMap[nums[i]] = 1;
            }
        }
        return -1;
    }
};
```


时间复杂度：O(n)。
空间复杂度：O(n)。




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
时间复杂度：O(n)。

空间复杂度：O(1)。
