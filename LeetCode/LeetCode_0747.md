# LeetCode_747 至少是其他数字两倍的最大数
在一个给定的数组nums中，总是存在一个最大元素 。

查找数组中的最大元素是否至少是数组中每个其他数字的两倍。

如果是，则返回最大元素的索引，否则返回-1。

## 解答
直接看代码。
```C++
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        int n = nums.size();
        if(n == 0) return -1;
        int max = nums[0];
        int maxIndex = 0;
        for (int i = 0; i < n; i++){
            if(max < nums[i]){
                max = nums[i];
                maxIndex = i;
            }
        }
        for (int i = 0; i < n; i++){
            if (i != maxIndex){
                if(max - nums[i] < nums[i]) return -1;
            }
        }
        return maxIndex;
    }
};
```