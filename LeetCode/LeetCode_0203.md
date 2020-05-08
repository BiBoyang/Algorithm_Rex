# LeetCode_203 移除链表元素
删除链表中等于给定值 val 的所有节点。

示例:
```C++
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *cur = dummy;
        while(cur->next) {
            if(cur->next->val == val) {
                cur->next = cur->next->next;
            } else {
                cur = cur->next;
            }
        }
        return dummy->next;
    }
};
```
* 时间复杂度：O(n)
* 空间复杂度：O(1)