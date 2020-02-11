
# LeetCode_0023 合并K个排序链表

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:

输入:
```C++
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

## 解答
#### 方法一
堆排序法
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        //自定义排序内容
        auto cmp = [](ListNode *a, ListNode *b) {
            return a->val > b->val;
        };
        //建立堆
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> heap(cmp);
        //遍历加堆
        for (auto node : lists) {
            if(node) { 
                heap.push(node);
            }
        }
        ListNode *dummy = new ListNode(0), *cur = dummy;
        //从堆中取出
        while (!heap.empty()) {
            auto t = heap.top();
            heap.pop();
            cur->next = t;
            cur = cur->next;
            if (cur->next) {
                heap.push(cur->next);
            }
        }
        return dummy->next;        
    }
};
```
时间复杂度： O(Nlog⁡k) ，其中 k 是链表的数目。
 * 弹出操作时，比较操作的代价会被优化到 O(log⁡k) 。同时，找到最小值节点的时间开销仅仅为 O(1)。
 * 最后的链表中总共有 N 个节点。

空间复杂度：O(n)。
创造一个新的链表需要 O(n) 的开销。



#### 方法二
分治。
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode* head = new ListNode(0); 
        ListNode* point = head; 
        for(int i=0; i<lists.size(); i++) {
            point->next = mergeTwoLists(point->next,lists[i]); 
        }
        return head->next;

    }
private:
    ListNode *mergeTwoLists(ListNode *l1,ListNode *l2) {
        if(l1 == NULL) {
             return l2;
        }
        if(l2==NULL) {
            return l1;
        }
        if(l1->val<l2->val) { 
            l1->next = mergeTwoLists(l1->next,l2); 
            return l1;
        } else { 
            l2->next = mergeTwoLists(l1,l2->next); 
            return l2; 
        }
    }
};
```

时间复杂度： O(Nlog⁡k) ，其中 k 是链表的数目。
空间复杂度：O(1)
