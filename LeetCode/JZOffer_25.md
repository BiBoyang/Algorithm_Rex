# 面试题25. 合并两个排序的链表
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：
```C++
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

# 解答
### 迭代法
归并排序
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode *res = new ListNode(0);
        ListNode *temp = res;
        while(l1 != NULL && l2 != NULL) {
            if(l1->val < l2->val) {
                temp->next = l1;
                l1 = l1->next;
            } else {
                temp->next = l2;
                l2 = l2->next;
            }
            temp = temp->next;
        }
        temp->next = l1 == NULL ? l2 : l1;
        return res->next;
    }
};
```
### 递归法
归并排序
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == NULL)
            return l2;
        if (l2 == NULL) 
            return l1;
        //归并排序的第三者
        ListNode *res = NULL;
        
        if(l1->val < l2->val) {
            res = l1;
            res->next = mergeTwoLists(l1->next,l2);  
        } else {
            res = l2;
            res->next = mergeTwoLists(l2->next,l1);
        }
        return res;
    }
};
```



### 使用堆

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        priority_queue<int, vector<int>, greater<int>> heap;
        while(l1) {
            heap.push(l1->val);
            l1 = l1->next;
        }
        while(l2){
            heap.push(l2->val);
            l2 = l2->next;
        }
       
        ListNode *temp = new ListNode(0);
        ListNode *res = temp;
        while (!heap.empty()) {
            int t = heap.top();
            //创建下一个结点
            temp->next = new ListNode(t);
            //把指针指向下一个结点
            temp = temp->next;
            heap.pop();
        }
        return res->next;
    }
};
```