# LeetCode_82 删除排序链表中的重复元素 II
给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:
```
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```

示例 2:
```
输入: 1->1->1->2->3
输出: 2->3
```

# 解答
## 递归法
```C++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        if(head ==NULL) return head;
        if(head->next && head->val == head->next->val) {
            while(head && head->next && head->val == head->next->val) {
                head = head->next;
            }
            //这里直接跳过，走next
            return deleteDuplicates(head->next);
        } else {
            head->next = deleteDuplicates(head->next);
        }       
        return head;
    }
};
```
## 双指针法
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
    ListNode* deleteDuplicates(ListNode* head) {
        //快慢指针
        if(head == NULL ) return head;
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *slow = dummy;
        ListNode *fast = dummy->next;
        while(fast) {
            if(fast->next && fast->val == fast->next->val )  {
                int temp = fast->val;
                while(fast && temp == fast->val) {
                    fast = fast->next;
                }
            } else {
                slow->next = fast;
                slow = fast;
                fast = fast->next;
            }

            slow->next = fast;
        
        }
        return dummy->next;
    }
};
```