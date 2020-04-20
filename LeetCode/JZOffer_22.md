# 面试题22. 链表中倒数第k个节点

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

 

示例：
```C++
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

# 解答

这道题可以使用双指针法。

使用 left 和 right 两个指针，然后让 right 指针先走 k 次。
然后再一起走， right 一旦到头，left 也就会正好在那个位置上。
```C++
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode *left = head,*right = head;
        for(int i = 0;i<k;i++) {
            right = right->next;
        }
        while(right != NULL) {
            left = left->next;
            right = right->next;
        }
        return left;
    }
};
```

当然，也可以省略第一个 for 循环。
```C++
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode *left = head,*right = head;
        int t = 0;
        while(right != NULL) {
            if(t >= k) {
                left = left->next;
            }            
            right = right->next;
            t++;
        }
        return left;
    }
};
```