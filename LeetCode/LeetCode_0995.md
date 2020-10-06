# LeetCode_0995 K 连续位的最小翻转次数
在仅包含 0 和 1 的数组 A 中，一次 K 位翻转包括选择一个长度为 K 的（连续）子数组，同时将子数组中的每个 0 更改为 1，而每个 1 更改为 0。

返回所需的 K 位翻转的次数，以便数组没有值为 0 的元素。如果不可能，返回 -1。

 

示例 1：

输入：A = [0,1,0], K = 1
输出：2
解释：先翻转 A[0]，然后翻转 A[2]。

示例 2：

输入：A = [1,1,0], K = 2
输出：-1
解释：无论我们怎样翻转大小为 2 的子数组，我们都不能使数组变为 [1,1,1]。

示例 3：

输入：A = [0,0,0,1,0,1,1,0], K = 3
输出：3
解释：
翻转 A[0],A[1],A[2]: A变成 [1,1,1,1,0,1,1,0]
翻转 A[4],A[5],A[6]: A变成 [1,1,1,1,1,0,0,0]
翻转 A[5],A[6],A[7]: A变成 [1,1,1,1,1,1,1,1]

 

提示：

    1 <= A.length <= 30000
    1 <= K <= A.length

## 解答
时间复杂度： O(N)，其中 N 是数组 A 的长度。
空间复杂度： O(N)。
> 执行用时 : 64 ms, 在Minimum Number of K Consecutive Bit Flips的C++提交中击败了100.00% 的用户
> 内存消耗 : 18.9 MB, 在Minimum Number of K Consecutive Bit Flips的C++提交中击败了19.44% 的用户




我们采取逐渐缩小区间的方法来解决，目的是持续翻转，但是在翻转的同时将边上为1的数字移除，缩小范围（这一点上比较类似煎饼排序）。
我们最开始可以从下标为0的数字出发，判断它是否为0。假如它为1，我们就跳过它，因为我们对它的翻转是毫无意义的；如果为0，则从它开始翻转，翻转K区间内的所有数字，然后将变为1的首个数字移除，向右移，重复这个操作。

按照这个思路，我们写出了如下代码
```C++
class Solution {
public:
    int minKBitFlips(vector<int>& A, int K) {
        int ans = 0;
        int len = A.size();
        for(int i = 0;i< len ;i++) {
            if(A[i]==0) {
                ans++;
                for(int j=i;j<i+K;j++) {
                    if(i + K > len) return -1;
                    A[j] ^= 1;
                }
            }
        }
        return ans;
    }
};
```
很不幸，虽然思路是对的，但是有部分测试用例会超时。问题出在哪呢？
我们可以发现，在翻转A[i, i+K)部分，当次翻转范围与上次翻转范围存在重叠，当重叠部分进行翻转的两次的时候，相当于没有翻转，造成了时间的浪费。
那就继续优化它。
我们设置一个flip位来记录是否翻转，array数组来作为翻转记录。
flip ^= hint[i], 异或运算后flip位表示当前位置i是否被翻转过，flip=0,未翻转，flip=1,翻转。
判断A[i] == flip，这里会有两种情况
> 1. A[i]与flip均为0时，表示A[i] = 0且当前位未被翻转，需要进行翻转
> 2. A[i]与flip均为1时，表示A[i] = 1且当前位已被翻转（实际值为0），需要再次翻转
可见，如果相等，不管怎样，都是需要翻转的。
翻转之后，继续对flop进行翻转，表示此次翻转结束；然后对hint[i+K]位进行翻转，记录翻转范围。

举个例子：[0,1,1,1,1,0] 2
[1,0,1,1,1,0]
[1,1,0,1,1,0]
[1,1,1,0,1,0]
[1,1,1,1,0,0]
[1,0,1,1,1,1]

```C++
static const auto __ = [](){
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    return nullptr;
}();
class Solution {
public:
    int minKBitFlips(vector<int>& A, int K) {
        int len = A.size();
        vector<int> array(len,0);
        int res = 0,flip = 0;
        for(int i = 0;i < len;i++) {
            flip ^= array[i];
            if(A[i] == flip) {
                if(i + K > len) return -1;
                res++;
                flip ^= 1;
                if(i+K < len) array[i+K] ^= 1;   
            }   
        }
        return res;
    }
};
```