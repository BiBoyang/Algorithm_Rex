
# LeetCode_0001 两数之和

难度**easy**

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:
```C++
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

# 标准答案

## 1. 哈希法
我们理解题意，可知，可以知道一个数字在和为target的情况下，有唯一一个对应的数字。
我们可以先进行遍历，将每个数字加入到一个哈希表当中，然后在第二次遍历当中去匹配另外一个数字。


时间复杂度：
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        //创建一个哈希表        
        unordered_map<int, int> hashTwoMap;
        //创建一个数组用于记录和输出结果
        vector<int> res;
        //首次遍历将每个数字在哈希表中打锚
        for (int i = 0; i < nums.size(); ++i)
         {
            hashTwoMap[nums[i]] = i;
        }
        //二次遍历，查找 target-x 对应的数字是否存在        
        for (int i = 0; i < nums.size(); ++i) 
        {
            int t = target - nums[i];
            //这里第一个判断是保证 t 数字出现过
            //这里第二个判断是保证 这个数字不在原有的位置上（即可能出现两个数字一样的情况），这个细节非常重要！！！
            if (hashTwoMap.count(t) != 0 && hashTwoMap[t] != i)
            {
                res.push_back(i);
                res.push_back(hashTwoMap[t]);
                break;
            }
        }
        return res;
    }
};
```
* 时间复杂度：O(n)， 我们把包含有 n 个元素的列表遍历两次。由于哈希表将查找时间缩短到 O(1) ，所以时间复杂度为 O(n)。
* 空间复杂度：O(n)。无需多言，哈希表的解决方法的空间复杂度多是如此。

## 2.优化过后的哈希法
在上一步中，我们分两次给哈希表进行添加和甄别。
我们其实可以直接在一次中直接进行这两步操作。

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int>hashTwoMap;
        vector<int>res;
        //一次遍历，查找 target-x 对应的数字是否存在        
        for (int i = 0; i < nums.size(); ++i) 
        {
            int t = target - nums[i];
            //判断对应的数字在哈希表中是否存在
            if(hashTwoMap.count(nums[i]) !=0)
            {
                res.push_back(hashTwoMap[nums[i]]);
                res.push_back(i);
                break;
            }
            //将对应的 target-x 插入哈希表中
            hashTwoMap[t] = i;
        }
        return res;
    }
};
```

