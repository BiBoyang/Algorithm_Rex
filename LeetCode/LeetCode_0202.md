# LeetCode_0202 快乐数
编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。如果 可以变为  1，那么这个数就是快乐数。

如果 n 是快乐数就返回 True ；不是，则返回 False 。

示例：
```
输入：19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

# 解答
## 方法一
算法分为两部分，我们需要设计和编写代码。

给一个数字 n，它的下一个数字是什么？
按照一系列的数字来判断我们是否进入了一个循环。
第 1 部分我们按照题目的要求做数位分离，求平方和。

第 2 部分可以使用 HashSet 完成。每次生成链中的下一个数字时，我们都会检查它是否已经在 HashSet 中。

如果它不在 HashSet 中，我们应该添加它。
如果它在 HashSet 中，这意味着我们处于一个循环中，因此应该返回 false。
我们使用 HashSet 而不是向量、列表或数组的原因是因为我们反复检查其中是否存在某数字。检查数字是否在哈希集中需要 O(1)O(1) 的时间，而对于其他数据结构，则需要 O(n) 的时间。选择正确的数据结构是解决这些问题的关键部分。

```C++
class Solution {
public:
    int getNext(int n) {
        int totalSum = 0;
        while (n > 0) {
            int d = n % 10;
            n = n / 10;
            totalSum = totalSum + d * d;
        }
        return totalSum;
    }
    bool isHappy(int n) {
        unordered_set<int> hashSet;
        while(n != 1 && hashSet.count(n) ==0 ) {
            hashSet.insert(n);
            n = getNext(n);
        }
        return n == 1;
    }
};
```
* 时间复杂度：O(logN)；
* 空间复杂度：O(logN)


## 方法二：
快慢指针的方法
```C++
class Solution {
public:
    int getNext(int n) {
        int totalSum = 0;
        while (n > 0) {
            int d = n % 10;
            n = n / 10;
            totalSum = totalSum + d * d;
        }
        return totalSum;
    }
    bool isHappy(int n) {
        int slow = n;
        int fast = getNext(n);
        while(fast != 1 && slow != fast) {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        }
        return fast == 1;
    }
};
```
* 时间复杂度：O(logN)
* 空间复杂度：O(1)
