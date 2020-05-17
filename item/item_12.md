# 链表刷题之旅（六）：合并有序链表

合并链表是一个很考虑思维的题。

先从合并两个链表来看。

# 合并两个有序链表

做这个题，最开始还是比较经典的，先判空。
```C++
if (l1 == NULL) return l2;
if (l2 == NULL) return l1;
```

使用递归的话，非常容易理解。我们要判断 l1 和 l2 哪一个的头元素更小，然后递归地决定下一个添加到结果里的值。如果两个链表都是空的，那么过程终止，所以递归过程最终一定会终止。

代码就如下所示。

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

* 时间复杂度：O(m+n)
* 空间复杂度：O(m+n)。调用 mergeTwoLists 退出时 l1 和 l2 中每个元素都一定已经被遍历过了，所以 n+m个栈帧会消耗 O(n+m) 的空间。

那么，如果不想使用递归的话，也可新建一个链表，然后依次判断两个链表的大小，依次往下排列下去；一旦一个链表排列结束，就可以直接在新建的链表后面接上另外一个链表。

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


好了，合并两个排序链表实际上很简单，那么合并




