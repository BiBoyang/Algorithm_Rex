# 相交链表

编写一个程序，找到两个单链表相交的起始节点。

# 解答

## 哈希表
```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode *> s;
        ListNode *curA = headA;
        while(curA) {
            s.insert(curA);
            curA = curA->next;
        }
        ListNode *curB = headB;
        while(curB) {
            if(s.find(curB) != s.end()) {
                return curB;
            }
            curB = curB->next;
        }
        return NULL;
    }
};
```
* 时间复杂度：O(m+n)。
* 空间复杂度：O(m)或者O(n)。


## 双指针

1. 指针 pA 指向 A 链表，指针 pB 指向 B 链表，依次往后遍历
2. 如果 pA 到了末尾，则 pA = headB 继续遍历
3. 如果 pB 到了末尾，则 pB = headA 继续遍历
4. 比较长的链表指针指向较短链表head时，长度差就消除了

```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *a = headA;
        ListNode *b = headB;
        while(a != b) {
            if(a) {
                a = a->next;
            } else {
                a = headB;
            }
            if(b) {
                b = b->next;
            } else {
                b = headA;
            }
        }
        return a;
    }
};
```
* 时间复杂度：O(m+n)。
* 空间复杂度：O(1)。