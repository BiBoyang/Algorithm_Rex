# 链表刷题之旅（四）：

# 奇偶链表
给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。
## 解答
是把链表分成两条：一条奇数，一条偶数，这应该算是最朴素的想法了然后把它们连起来
所以我做了如下操作：
* 第一步：头节点肯定是奇数节点，这毋庸置疑。所以 odd = head，把头节点拿出来当奇数链表的头节点
* 第二步：头节点的下一个节点肯定是偶数节点了，所以 even = head.next，把 head.next 拿出来当偶数链表的头节点，这里要注意了，一定要把偶数链表的头节点单独拿出来，这里我后面详细说
* 第三步：找出关系式，奇数链表的下下个节点才会是奇数节点，同样偶数节点的下下个节点才会是偶数节点

```C++
odd->next = odd->next->next;
even->next = even->next->next;
```

 * 第四步：找循环终止的条件
even && even->next 有一个为空

* 第五步：拿出头结点
odd->next = evenHead;



```C++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head == NULL) return NULL;
        ListNode *odd = head,*even = head->next,*evenHead = even;
        while(even && even->next) {
            odd->next = odd->next->next;
            even->next = even->next->next;
            odd = odd->next;
            even = even->next;
        }
        odd->next = evenHead;
        return  head;
    }
};
```


# 回文链表

