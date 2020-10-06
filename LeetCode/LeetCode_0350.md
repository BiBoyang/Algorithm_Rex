# LeetCode_350 两个数组的交集 II
给定两个数组，编写一个函数来计算它们的交集。

示例 1:

> 输入: nums1 = [1,2,2,1], nums2 = [2,2]
> 输出: [2,2]

示例 2:

> 输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
> 输出: [4,9]

说明：
> 输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
> 我们可以不考虑输出结果的顺序。

进阶:
> 如果给定的数组已经排好序呢？你将如何优化你的算法？
> 如果 nums1 的大小比 nums2 小很多，哪种方法更优？
> 如果 nums2 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

## 答案
#### hash
```
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res;
        unordered_map<int, int> hashmap;
        for(int i = 0; i != nums1.size(); i++){
            hashmap[nums1[i]]++;
        }
        for(int i = 0; i != nums2.size(); i++) {
            if(hashmap[nums2[i]] > 0 ) {
                res.push_back(nums2[i]);
                hashmap[nums2[i]]--;
            }
        }
    return res;
    }
};
```

## 扩展
加入给定的数组已经排好序了。
可以使用两个指针，分别位于两个数组的首位。
```
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        //如果已经排好序了,使用双指针法
        vector<int> res;
        int cur1 = 0, cur2 = 0; // 定义指针，指向数组开始位置
        while (cur1 < nums1.size() && cur2 < nums2.size()) { 
            int num1 = nums1[cur1];
            int num2 = nums2[cur2];
            if(num1 == num2) {
                res.push_back(num1);
                cur1++;
                cur2++;
            }else if(num1 < num2) {
                cur1++;
            }else if(num1 > num2) {
                cur2++;
            } 
        }
        return res;
    }
};
```

如果nums1的大小小于nums2，则应该选择第二种方法，最慢也是和hash法持平（在排好序的情况下）。

