# LeetCode_707 设计链表

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

* get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
* addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
* addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
* addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
* deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。


示例：
```
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
```

# 解答

```C++
struct myListNode {
	int val;
	myListNode* next;
	myListNode() :val(-1), next(nullptr) {}
};


class MyLinkedList {
public:
	/** Initialize your data structure here. */
	MyLinkedList() :m_size(0) {
		m_head = new myListNode();
	}

	/** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
	int get(int index) {
		if (index > m_size - 1 || index < 0) {
			return -1;
		}
		myListNode* p = m_head->next;
		while (index != 0) {
			p = p->next;
			--index;
		}
		//std::cout << p->val;
		return p->val;
	}

	/** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
	void addAtHead(int val) {
		myListNode* newNode = new myListNode();
		newNode->next = m_head->next;
		m_head->next = newNode;
		newNode->val = val;
		m_size += 1;
	}

	/** Append a node of value val to the last element of the linked list. */
	void addAtTail(int val) {
		myListNode* lastNode = new myListNode();
		lastNode->val = val;
		myListNode* p = m_head;
		int len = m_size;
		while (len != 0)
		{
			p = p->next;
			--len;
		}
		p->next = lastNode;
		lastNode->next = NULL;
		m_size += 1;
	}

	/** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
	void addAtIndex(int index, int val) {
		if (index > m_size) return;
		if (index == m_size) {
			addAtTail(val);
			return;
		}
		if (index < 0) {
			addAtHead(val);
			return;
		}
		myListNode* newNode = new myListNode();
		myListNode* p = m_head;
		while (index != 0) {
			p = p->next;
			--index;
		}
		newNode->next = p->next;
		p->next = newNode;
		newNode->val = val;
		m_size += 1;
	}

	/** Delete the index-th node in the linked list, if the index is valid. */
	void deleteAtIndex(int index) {
		if (index > m_size - 1 || index < 0) return;
		myListNode* p = m_head;
		while (index != 0) {
			p = p->next;
			--index;
		}
		myListNode* delNode = p->next;;
		p->next = p->next->next;
		m_size -= 1;
		delete delNode;
	}
public:
	int m_size;
	myListNode* m_head;
	myListNode* m_tail;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```