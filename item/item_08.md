# 链表刷题之旅（二）

# 反转链表 I

反转一个单链表。
## 解答
### 迭代法
在遍历列表时，将当前节点的 next 指针改为指向前一个元素。由于节点没有引用其上一个节点，因此必须事先存储其前一个元素。在更改引用之前，还需要另一个指针来存储下一个节点。不要忘记在最后返回新的头引用！



```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *tempNode = NULL;;
        ListNode *currentNode = head;

        while(currentNode != NULL) {
            ListNode *nextNode = currentNode->next;
            currentNode->next = tempNode;
            tempNode = currentNode;
            currentNode = nextNode;
        }
        return tempNode;
    }
};
```


### 递归法
1. 使用递归函数，一直递归到链表的最后一个结点，该结点就是反转后的头结点，记作 temp .
2. 此后，每次函数在返回的过程中，让当前结点的下一个结点的 next 指针指向当前节点。
3. 同时让当前结点的 next 指针指向 NULL ，从而实现从链表尾部开始的局部反转
4. 当递归函数全部出栈后，链表反转完成。

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL || head->next == NULL) return head;
        ListNode *temp = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return temp;
    }
};
```

# 反转链表 II



# 移除链表元素
# 奇偶链表
# 回文链表
