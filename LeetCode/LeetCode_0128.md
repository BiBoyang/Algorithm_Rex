# LeetCode_0128. 最长连续序列

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

示例:
```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```


# 解答

```C++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        //哈希法
        unordered_set<int> hashSet;
        for(auto i:nums) {
            hashSet.insert(i);
        }
        int maxLen = 0;
        for(int i = 0;i< nums.size();i++) {
            if(hashSet.count(nums[i]-1)) {
                continue;
            } else {
                int temp=nums[i]+1;
                int count=1;
                while(hashSet.count(temp)) {
                    temp++;
                    count++;
                }
                maxLen = max(maxLen,count);
            }
            
            
        }
        
        return maxLen;
        
    }
};
```
