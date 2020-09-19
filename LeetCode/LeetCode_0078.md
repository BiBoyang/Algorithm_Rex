# LeetCode_0078 子集

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:
```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# 解答

使用递归回溯。


1. 初始化 temp 数组为空，并塞入结果数组 ans;
2. 递归调用 dfs 函数。



```C++
class Solution {
public:
    vector<int> temp;
    vector<vector<int>> ans;
    void dfs(vector<int>& nums, int index){
        ans.push_back(temp);
        for(int i = index + 1; i < nums.size(); i ++){
            temp.push_back(nums[i]);
            dfs(nums, i);
            temp.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        int n = nums.size();
        dfs(nums, -1);
        return ans;
    }
};

```
