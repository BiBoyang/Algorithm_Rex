# LeetCode_83 删除排序链表中的重复元素
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:
```
输入: 1->1->2
输出: 1->2
```

示例 2:
```
输入: 1->1->2->3->3
输出: 1->2->3
```
# 解答


```C++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *cur = head;
        while(cur && cur->next) {
            if(cur->next->val == cur->val) {
                cur->next = cur->next->next;
            } else {
                cur = cur->next;
            }
        }
        return head;
    }
};
```
* 时间复杂度：O(n)
* 空间复杂度：O(1)