# LeetCode_0349 两个数组的交集
给定两个数组，编写一个函数来计算它们的交集。

 

**示例 1：**
```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```
**示例 2：**
```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
``` 

**说明：**

* 输出结果中的每个元素一定是唯一的。
* 我们可以不考虑输出结果的顺序。

# 解答

```C++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> res;
        unordered_set<int> hashSet1(nums1.begin(),nums1.end());
        for(int num:nums2) {
            if(hashSet1.count(num) > 0) {
                res.insert(num);
            }
        }
        return vector<int>(res.begin(),res.end());
    }
};
```

* 时间复杂度：O(m+n)
* 空间复杂度：O(m+n)
