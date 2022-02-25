# 面试题 17.14. 最小K个数

设计一个算法，找出数组中最小的k个数。以任意顺序返回这k个数均可。

示例：

输入： arr = [1,3,5,7,2,4,6,8], k = 4
输出： [1,2,3,4]

# 解答

使用小顶堆

```C++

class Solution {
public:
    vector<int> smallestK(vector<int>& arr, int k) {
        vector<int> ans;
        priority_queue<int, vector<int>, greater<int>> que;

        for(int i = 0;i < arr.size();i++) {
            que.push(arr[i]);
        }
        for(int i = 0;i < k;i++){
            int cur = que.top();
            ans.push_back(cur);
            que.pop();
        }
        return ans;
    }
};
```

* 时间复杂度：O(nlogK)。n 是数组 arr 的长度。
* 空间复杂度：o(k)