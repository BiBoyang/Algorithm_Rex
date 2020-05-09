# 234. 回文链表

请判断一个链表是否为回文链表。

示例 1:
```
输入: 1->2
输出: false
```
示例 2:
```
输入: 1->2->2->1
输出: true
```
# 解答
这里有两种方法，先说难的。
## 双指针法
我们可以将链表的后半部分反转（修改链表结构），然后将前半部分和后半部分进行比较。比较完成后我们应该将链表恢复原样。虽然不需要恢复也能通过测试用例，因为使用该函数的人不希望链表结构被更改。

算法：

我们可以分为以下几个步骤：

1. 找到前半部分链表的尾节点。
2. 反转后半部分链表。
3. 判断是否为回文。
4. 恢复链表。
5. 返回结果。

执行步骤一，我们可以计算链表节点的数量，然后遍历链表找到前半部分的尾节点。

或者可以使用快慢指针在一次遍历中找到：慢指针一次走一步，快指针一次走两步，快慢指针同时出发。当快指针移动到链表的末尾时，慢指针到链表的中间。通过慢指针将链表分为两部分。

若链表有奇数个节点，则中间的节点应该看作是前半部分。

步骤二可以使用在反向链表问题中找到解决方法来反转链表的后半部分。

步骤三比较两个部分的值，当后半部分到达末尾则比较完成，可以忽略计数情况中的中间节点。

步骤四与步骤二使用的函数相同，再反转一次恢复链表本身。

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
    bool isPalindrome(ListNode* head) {
        if(head == NULL || head->next == NULL) return true;
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        //翻转
        ListNode *cur = slow;
        ListNode *cur_next = slow->next;
        while(cur_next) {
            ListNode *temp = cur_next->next;
            cur_next->next = cur;
            cur = cur_next;
            cur_next = temp;
        }
        slow->next = NULL;

        //比较
        while(head && cur) {
            if(head->val != cur->val){
                return false;
            }
            head  = head->next;
            cur = cur->next;
        }
        return true;
    }
};
```

## 转换成数组
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
    bool isPalindrome(ListNode* head) {
        vector<int> nodeArray;
        while(head) {
            nodeArray.push_back(head->val);
            head = head->next;
        }
        int len = nodeArray.size();
        for(int i = 0;i<len;i++) {
            if(nodeArray[i] != nodeArray[len-1-i]){
                return false;
            }
        }
        return true;
    }
};
```
