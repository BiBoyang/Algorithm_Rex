# LeetCode_141 环形链表

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

# 解答
使用快慢指针。
```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if(slow == fast) {
                return true;
            }
        }
        return false;
    }
};
```

* 时间复杂度：O(n)。
        假如有环，快指针将会首先到达尾部，其时间取决于列表的长度，也就是 O(n)。
        假如无环，时间复杂度会是O(N+K)。K 是环形长度。
* 空间复杂度：O(1)。