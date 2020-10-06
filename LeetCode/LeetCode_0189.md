# LeetCode_189 旋转数组
给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:

> 输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

示例 2:
> 输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]

说明:
> * 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
> * 要求使用空间复杂度为 O(1) 的原地算法。

## 答案
#### 方法一

我们可以简单的将这个问题看成，在n-k次里把后边的数字一个一个搬到了前面。可以直接利用STL的push_back和erase方法实现这个搬运工作。
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (nums.empty() || (k %= nums.size()) == 0) return;
        int n = nums.size();
        for (int i = 0; i < n - k; ++i) {
            nums.push_back(nums[0]);
            nums.erase(nums.begin());
        }  
    }
};
```


#### 方法二：
利用reverse函数进行翻转，这种方法其实比较多见于字符串的翻转，这里我们拿来。
前n-k个数字先进行翻转，然后后k个数字进行翻转，最后将整个数组都翻转一遍。

```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        
        if (nums.empty() || (k %= nums.size()) == 0) 
            return;
        int len = nums.size();
        reverse(nums.begin(), nums.begin() + len - k);
        reverse(nums.begin() + len - k, nums.end());
        reverse(nums.begin(), nums.end());
        
    }
};
```

#### 方法三：
我们还可以通过循环交换数字位置来实现旋转
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (nums.empty()) return;
        int n = nums.size(), start = 0;   
        while (n && (k %= n)) {
            for (int i = 0; i < k; ++i)
            {
                swap(nums[i + start], nums[n - k + i + start]);
            }
            n -= k;
            start += k;
        }
    }
};
```
可以简单的理解为，交换k次数字来实现最后的结果，缺点也可想而知，都要交换k次。

#### 扩展思路：

如果不考虑空间复杂度的情况下，我们也可以采用临时数组的方式来进行映射。
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> a = nums;
        for (int i = 0; i < nums.size(); ++i)
         {
            nums[(i + k) % nums.size()] = a[i];
        }
    }
};
```

或者同样的思路

```C++
//比较简单的思路：构建一个新的数组，然后把旧数组值转换给新数组，最后把新数组赋值给旧数组

class Solution {
public:
    void rotate(vector<int>& nums, int k) { 
        if(nums.empty()) 
        {
            return;
        }
        int len=nums.size(); 
       
        if(k>nums.size()) 
        {
            k = k % len; 
        } 
        vector<int>temp; 
        for (int i=len-k;i<len;++i) 
        {
            temp.push_back(nums[i]); 
        }
        for (int j=0;j<len-k;++j)
        {
            temp.push_back(nums[j]);
        }
        nums=temp;
    }
};

```