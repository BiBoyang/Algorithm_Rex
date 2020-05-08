# LeetCode_92 反转链表 II

反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

说明:
1 ≤ m ≤ n ≤ 链表长度。

示例:
```C++
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

# 解答

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        if(m == n) return head;
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *a = dummy,*b = dummy;
        for(int i = 0;i< m-1;i++) {
            a = a->next;
        }
        for(int i = 0;i<n;i++) {
            b = b->next;
        }
        ListNode *c = a->next,*d = b->next;
        for(auto tempA = c,tempB = tempA->next;tempB != d;) {
            auto tempC = tempB->next;
            tempB->next = tempA;
            tempA = tempB;
            tempB = tempC;
        }
        a->next = b;
        b->next = d;

        return dummy->next;
    }
};
```
