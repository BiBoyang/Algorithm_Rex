# LeetCode_796 旋转字符串
给定两个字符串, A 和 B。

A 的旋转操作就是将 A 最左边的字符移动到最右边。 例如, 若 A = 'abcde'，在移动一次之后结果就是'bcdea' 。如果在若干次旋转操作之后，A 能变成B，那么返回True。

示例 1:
```
输入: A = 'abcde', B = 'cdeab'
输出: true
```
示例 2:
```
输入: A = 'abcde', B = 'abced'
输出: false
```
注意：
* A 和 B 长度不超过 100。

## 解答
#### 方法一
暴力法
```
class Solution {
public:
    bool rotateString(string A, string B) {
        if(A=="" && B=="") return true;
        int lenA = A.size();
        int lenB = B.size();
        if(lenA != lenB) return false;
        for(int i = 0 ; i < lenA;i++) {
            char temp = A[0];
            for(int j = 0 ; j <lenA-1; j++) {
                A[j] = A[j+1]; 
            }
            A[lenA-1] = temp;
            if(A == B) return true;
        }
        return false;
    }
};
```

#### 方法二
创建一个字符串C，C等于两个A连接起来
```
class Solution {
public:
    bool rotateString(string A, string B) {
        if(A=="" && B=="") return true;
        int lenA = A.size();
        int lenB = B.size();
        if(lenA != lenB) return false;
        string C = A + A;
        for(int i = 0;i < lenA;i++) {
            int j = 0;
            if(C[i] == B[j]) {
                while(j < lenA) {
                    if(C[i + j] == B[j]) {
                        j++;
                    } else {
                        break;
                    }
                }
                if(j == lenA) return true;   
            }   
        }
        return false;
    }
};
```