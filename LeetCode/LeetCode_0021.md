
# LeetCode_0021 合并两个有序链表

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
```C++
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

# 解答
## 递归法

如果 l1 或者 l2 一开始就是 null ，那么没有任何操作需要合并，所以我们只需要返回非空链表。否则，我们要判断 l1 和 l2 哪一个的头元素更小，然后递归地决定下一个添加到结果里的值。如果两个链表都是空的，那么过程终止，所以递归过程最终一定会终止。

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
或者更简单一点
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL) {
            return l2;
        } else if(l2 == NULL) {
            return l1;
        } else if(l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next =  mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```
* 时间复杂度：O(m+n)
* 空间复杂度：O(m+n)。调用 mergeTwoLists 退出时 l1 和 l2 中每个元素都一定已经被遍历过了，所以 n+m个栈帧会消耗 O(n+m) 的空间。



## 迭代法
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

* 时间复杂度：O(m+n)
* 空间复杂度：O(1)
