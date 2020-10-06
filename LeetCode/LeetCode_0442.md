# LeetCode_442 数组中重复的数据
给定一个整数数组 a，其中1 ≤ a[i] ≤ n （n为数组长度）, 其中有些元素出现两次而其他元素出现一次。
找到所有出现两次的元素。
你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？
示例：
> 输入:
> [4,3,2,7,8,2,3,1]
> 输出:
> [2,3]
  
  

## 标准答案
交换法。
遍历整个数组，然后重排数组。 
当遍历到下标为i的数字时，首先比较这个数字（用m表示）是不是等于i。
如果是，就继续遍历下一个数字；如果不是，则拿它和第m个数字进行比较。
如果相等，则表示一个重复的数字；如果不相等，则交换这两个数字。并继续比较。

```C++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> ans;
        for(int i=0;i<nums.size();i++) {
            if(nums[i] == nums[nums[i]])
                ans.push_back(nums[i]);
            //swap(nums[i],nums[nums[i]-1]);
            int temp = nums[i];
            nums[i] = nums[temp];
            nums[temp] = temp;
        }    
    return ans;
    }
};
``` 
  
## 扩展
在并不强求时间复杂度和空间复杂度的情况下，还有其他几种方法可以寻找出 *全部* 的重复数字。

#### hash法
这个方法简单明了，利用hashTable的特点，直接找出重复的数字，时间复杂度是O(1)，但是代价是一个O(n)大小的哈希表。

> 实际上，这个方法才是在App制作中最经常使用的和最应该使用的，App中的时间的重要性要远远大于对空间的。

```C++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
	std::unordered_map<int, int> hashmap = {};   
    vector<int> ans;
    for(int i=0;i<nums.size();i++) {
        if(hashmap[nums[i]] == 0) {
            hashmap[nums[i]]++;
        } else {
            ans.push_back(nums[i]);
        }
    }
     return ans;
    }
};
```