# LeetCode_0148. 排序链表

在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

示例 1:
```
输入: 4->2->1->3
输出: 1->2->3->4
```
示例 2:
```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

# 解答

```C++
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if(!head || !head->next) {
            return head;
        }
        //快慢双指针找中点
        ListNode *left = head, *mid = head, *right = head;
        while(right && right->next) {
            right = right->next->next;
            mid = left;
            left = left -> next;
        }
        mid -> next = nullptr;
        return merge(sortList(head),sortList(left));
        
    }
private:
    ListNode *merge(ListNode *node1,ListNode *node2) {
        //归并排序
        if(!node1) return node2;
        if(!node2) return node1;
        if(node1->val <= node2->val) {
            node1->next = merge(node1->next,node2);
            return node1;
        } else {
            node2->next = merge(node2->next,node1);
            return node2;
        }
    }
};
```