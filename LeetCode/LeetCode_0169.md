
# LeetCode_0169 多数元素

给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:
```
输入: [3,2,3]
输出: 3
```
示例 2:
```
输入: [2,2,1,1,1,2,2]
输出: 2
```

# 解答
## 方法一：哈希法
马上就能想到的方法就是使用哈希表。
用一个循环遍历数组 nums 并将数组中的每个元素加入哈希映射中。在这之后，我们遍历哈希映射中的所有键值对，返回值最大的键。
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> hashMap;
        int major = 0,count = 0;
        for(int num : nums) {
            hashMap[num]++;
            if(hashMap[num] > count) {
                major = num;
                count = hashMap[num];
            }
        }
        return major;
    }
};
```
时间复杂度：O(n)。n是nums的长度。
空间复杂度：O(n)。

## 方法二：排序
这里有几种方式，最简单的方法是直接使用C++自带的排序算法。
这里C++原生的sort函数，实际上并不是简单的快速排序，可以视为优化过的排序算法。
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
         sort(nums.begin(),nums.end());
         return nums[nums.size()/2];
    }
};
```
时间复杂度：O(nLogn)。
空间复杂度：O(logn)，因为是自带的排序，实际上需要占空间。


此外，还可以使用堆排序。


```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        auto cmp = [](int a,int b) {
            return a > b;
        };
        priority_queue<int,vector<int>,decltype(cmp)> heap(cmp);
        for(auto num : nums) {
            heap.push(num);
        }
        while(heap.size() > (nums.size() + 1) / 2) {
            heap.pop();
        }
        return heap.top();
    }
};

```
空间复杂度：O(nlogn)。
构建堆的时候空间复杂度为O(n)，在交换并重建堆的过程中，需交换n-1次，而重建堆的过程中，根据完全二叉树的性质，[log2(n-1),log2(n-2)...1]逐步递减，近似为nlogn。
空间复杂度：o(n)。


## 方法三：随机数算法。
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        while(true) {
            int candidate = nums[rand() % nums.size()];
            int count = 0;
            for(int num : nums) {
                if(num == candidate) {
                    count++;
                }
            }
            if(count > nums.size() / 2) {
                return  candidate;
            }
        }
        return -1;
    }
};
```

时间复杂度：O(n)。
空间复杂度：O(1)。


## 方法四:投票法。
摩尔投票法。投我++，不投--。
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0,value = 0;
        for(int i = 0;i<nums.size();i++) {
            if(count == 0) {
                value = nums[i];
                count++;
            } else if(value == nums[i]){
                count++;
            } else {
                count--;
            }
        }
        return value;
    }
};
```

## 方法五：位运算。
```C++

```