
# LeetCode_0015 三数之和

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]

# 解答
看起来是三个数的和，我们可以把它转换成两数之和的问题。
先将它排序，然后我们再取出一个target，设置两个指针i，j。
将问题转化成i+j = -target的问题。
这里可以分为几步：

> 1. 先对数组进行排序
> 2. 然后进行边界判断，如果第一个数是大于0的，则说明所有的数都大于0；如果最后一个数小于0，则说明所有的数都小于0.
> 3. 然后遍历整个数组，假如遇到了相同的两个数字，我们就越过后一个。
> 4. 然后设置左右双指针，遇到正确的数字就加入结果中。然后左指针右移，右指针左移；如果结果小于 target的话，我们就只右移左指针；如果结果大于target，就左移右指针。
> 5. 在遇到正确的数字的时候，我们还需要再做一次重复数字剔除。


```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        //先进行排序
        sort(nums.begin(), nums.end());
        /*
        * 边界判断，如果最后一个数字小于0，或者第一个数字大于0，则说明不会存在结果
        */
        if (nums.empty() || nums.back() < 0 || nums.front() > 0) 
            return {};
        for (int k = 0; k < nums.size(); ++k) {
            if (nums[k] > 0) 
                break;
            //排序后的结果中，如果有连续两个相同的数字，则跳过判断，以免重复
            if (k > 0 && nums[k] == nums[k - 1]) 
                continue;
            int target = 0 - nums[k];
            //前后双指针
            int i = k + 1, j = nums.size() - 1;
            while (i < j) {
                if (nums[i] + nums[j] == target) {
                    res.push_back({nums[k], nums[i], nums[j]});
                    //剔除重复数字的过程
                    while (i < j && nums[i] == nums[i + 1]) 
                        ++i;
                    while (i < j && nums[j] == nums[j - 1])
                        --j;
                    ++i; 
                    --j;
                } else if (nums[i] + nums[j] < target) 
                    ++i;
                else 
                    --j;
            }
        }
        return res;
    }
};
```