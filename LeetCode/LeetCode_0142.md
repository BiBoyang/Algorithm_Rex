# LeetCode_0142 环形链表 II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

# 解答
假如没有相遇，则直接输出 NULL。

假如有相遇，说明肯定有环。这时氛围两个阶段：

**第一阶段：**

* 设链表共有 a+b个节点，其中 链表头部到链表入口 有 a 个节点（不计链表入口节点）， 链表环 有 b 个节点；设两指针分别走了 f，s 步，则有：
    1. fast 走的步数是slow步数的 22 倍，即 f=2s；（解析： fast 每轮走 2 步）
    2. fast 比 slow 多走了 n 个环的长度，即 f=s+nb ；（解析： 双指针都走过 a 步，然后在环内绕圈直到重合，重合时 fast 比 slow 多走环的长度整数倍）；

* 以上两式相减得：f=2nb，s = nb，即 fast和slow 指针分别走了 2n，n 个 环的周长 （注意：n 是未知数，不同链表的情况不同）。

**第二阶段：**

给定阶段 1 找到的相遇点，阶段 2 将找到环的入口。首先我们初始化额外的两个指针： left ，指向链表的头， right 指向相遇点。然后，我们每次将它们往前移动一步，直到它们相遇，它们相遇的点就是环的入口，返回这个节点。


```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head;
        ListNode *fast = head;

        while(true) {
            if( fast == NULL || fast->next == NULL) {
                return NULL;
            }
            slow = slow->next;
            fast = fast->next->next;
            if(slow == fast) break;
        }
        ListNode *left = head;
        ListNode *right = slow;
        while(left != right) {
            left = left->next;
            right = right->next;
        }
        return right;
    }
};
```

* 时间复杂度：O(n)
* 空间复杂度：O(1)。