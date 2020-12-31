# LeetCode_1005 K 次取反后最大化的数组和
给定一个整数数组 A，我们只能用以下方法修改该数组：我们选择某个个索引 i 并将 A[i] 替换为 -A[i]，然后总共重复这个过程 K 次。（我们可以多次选择同一个索引 i。）

以这种方式修改数组后，返回数组可能的最大和。

 

示例 1：
```
输入：A = [4,2,3], K = 1
输出：5
解释：选择索引 (1,) ，然后 A 变为 [4,-2,3]。
```
示例 2：
```
输入：A = [3,-1,0,2], K = 3
输出：6
解释：选择索引 (1, 2, 2) ，然后 A 变为 [3,1,0,2]。
```
示例 3：
```
输入：A = [2,-3,-1,5,-4], K = 2
输出：13
解释：选择索引 (1, 4) ，然后 A 变为 [2,3,-1,5,4]。
```
 

提示：
```
    1 <= A.length <= 10000
    1 <= K <= 10000
    -100 <= A[i] <= 100
```


# 答案

## 方法一
先把数组排序。然后把k视为资源，把小于 0 的数都取反，直到没有负数或者 k 消耗完毕。

```c++
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {
        sort(A.begin(),A.end());
        int sum = 0;
        for(int i = 0;i < A.size();i++){
            if(A[i] < 0) {
                A[i] = -A[i];
                K--;
            } else if(K % 2 == 1){
                if(i > 0) {
                    if(A[i] < A[i - 1]) {
                        A[i] = -A[i];
                    } else {
                        A[i -1] = -A[i-1]; 
                    }
                } else{
                    A[i] = -A[i];
                }
                K--;
            }
            if(K <= 0) break;
        }
        for(int i = 0;i <A.size();i++){
            sum += A[i];
        }
        return sum;
    }
};
```

## 方法二
堆排序方法。依然是贪心算法。

构建一个小顶堆，然后把所有的元素压入堆内，每次都取出最小的那个取反，直到执行完 K 次，这个时候会发现只有最小的那个数一直执行 取反操作。这样保证最大值。
```
class Solution {
public:
int largestSumAfterKNegations(vector<int> &A, int K) {  
    //创建一个升序堆
    priority_queue<int, vector<int>, greater<int> >heap;
    //加入堆中
    for (auto i : A)
        heap.push(i);
    for (int i = 0; i < K; ++i) {
        int t = heap.top();
        t *= -1;
        heap.pop();//删除堆首元素
        heap.push(t);//将t压入堆底部
    }
    int sum = 0;
    while (!heap.empty()) {
        sum += heap.top();
        heap.pop();
        }
    return sum;
    }
};
```
* 时间复杂度：O(n)。n 是 A 的大小。
* 空间复杂度：O(n)。