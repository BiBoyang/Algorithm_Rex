# LeetCode_905 按奇偶排序数组
给定一个非负整数数组 A，返回一个由 A 的所有偶数元素组成的数组，后面跟 A 的所有奇数元素。

你可以返回满足此条件的任何数组作为答案。

示例：
```
输入：[3,1,2,4]
输出：[2,4,3,1]
输出 [4,2,3,1]，[2,4,1,3] 和 [4,2,1,3] 也会被接受。
```
 

提示：

> 1.  **1 <= A.length <= 5000**
> 2.  **0 <= A[i] <= 5000**


## 答案

### 最简单的方法
我们重新建立一个数组，然后前后遍历原有数组,是偶数就加在最前面，是奇数就放到最后面。

```C++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
        int size = A.size();
        vector<int>result(size, 0);
        int first = 0, last = size - 1;
        for(int i = 0; i < size; i++) {
            if(A[i] % 2 == 0) {
                result[first ++] = A[i];
            } else {
                result[last--] = A[i]; 
            }
        }
        return result;
    }
};

```


### 双指针法
题意是要求将偶数放到奇数前面，且并不要求原有顺序，我们可以使用两个指针，分别从第一位向后移动和最后一位向前移动。在两个指针相遇之前，第一个指针始终是位于第二个指针前面的。如果第一个指针对应的是奇数，第二个指针对应的是偶数，我们就将两个数字交换。
```C++
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) {
        if(A.empty())
            return A;
        int len = A.size();
        int i = 0;
        int j = len - 1;
        
        while(i < j) {
            if(A[i] % 2 == 1 && A[j] % 2 == 0) {
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            } else if(A[i]%2==0) {
                i++;
            } else if(A[j]%2==1) {
                j--;
            }            
        }
        return A;
    }
};
```



