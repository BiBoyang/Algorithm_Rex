# LeetCode_0019 删除链表的倒数第N个节点

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：
```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```
说明：

给定的 n 保证是有效的。

# 解答

使用双指针法。
假设设定了双指针 p 和 q 的话，当 q 指向末尾的 NULL，p 与 q 之间相隔的元素个数为 n 时，那么删除掉 p 的下一个指针就完成了要求。

* 设置虚拟节点 dummy 指向 head
*  设定双指针 p 和 q，初始都指向虚拟节点 dummy
*  移动 q，直到 p 与 q 之间相隔的元素个数为 n
*  同时移动 p 与 q，直到 q 指向的为 NULL
*  将 p 的下一个节点指向下下个节点


```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
        ListNode *dummy = new ListNode(0);
        dummy->next = head;        
        ListNode*slow = dummy,*fast = dummy;
    
        for(int i=1;i <= n+1;i++) {
            fast = fast->next;
        }
        
        while(fast) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy->next;
    }
};
```