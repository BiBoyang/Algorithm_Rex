# LeetCode_0002 两数相加
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

> * 示例：		
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)		
输出：7 -> 0 -> 8		
原因：342 + 465 = 807		

## 解答
我们创建一个新的结点。然后去计算当前节点的两个数的和。如果小于10，则继续，如果大于10，则减10并做好进位标志。		
注意事项：
> 1.进入循环的时候每次都要把数字记录清空    
> 2.本轮数组加在一起过了10，要把bool标记留到下一轮中    
> 3.别忘了要创建下一个结点以及把指针指向下一个结点


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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *temp = new ListNode(0);
        ListNode *res = temp;
        bool isTenExc = false;//判断是否超过10
        int sum ;
        while(l1 || l2) {
            sum = 0;
            if(l1) {
                sum += l1->val;
                l1 = l1->next;
            }
            if(l2) {
                sum += l2->val;
                l2 = l2->next;
            }
            //记录上一轮的进位
            if(isTenExc) {
                sum += 1;
            }
            if(sum >= 10) {
                sum = sum % 10;
                isTenExc = true;
            } else {
                isTenExc = false;
            }  
            temp->next = new ListNode(sum);
            temp = temp->next;
        }
        if(isTenExc) {
            temp->next = new ListNode(1);
        } 
        return res->next;
    }
};

```