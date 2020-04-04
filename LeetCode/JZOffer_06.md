# 面试题06. 从尾到头打印链表
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

示例 1：
```
输入：head = [1,3,2]
输出：[2,3,1]
```

# 解答
## 解法一
直接使用递归。
```C++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        if(head == NULL) return {};
        res = reversePrint(head->next);
        res.push_back(head->val);
        return  res;
    }
};
```
时间复杂度：O(n)；
空间复杂度：O(n)。

## 解法二
使用了递归，当然也可以使用栈。
```C++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        stack<ListNode *> nodeStack;
        while(head) {
            nodeStack.push(head);
            head = head->next;
        }
        int len = nodeStack.size();
        
        for(int i = 0;i<len;i++) {
            ListNode *temp = nodeStack.top();
            nodeStack.pop();
            res.push_back(temp->val);
        }
        return res;
    }
};
```

时间复杂度：O(n)
空间复杂度：O(n)；