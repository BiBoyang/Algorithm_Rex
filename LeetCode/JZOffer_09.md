# 面试题09. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

示例 1：

输入：
```
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
示例 2：
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

# 解答

## 方案一
在添加的时候就做好准备

```C++
class CQueue {
public:
    stack<int> stack1;
    stack<int> stack2;
    int size;

    CQueue() {
    }
    
    void appendTail(int value) {
        while(!stack1.empty()) {
            stack2.push(stack1.top());
            stack1.pop();
        }
        stack1.push(value);
        while(!stack2.empty()) {
            stack1.push(stack2.top());
            stack2.pop();
        }
        size++;
    }
    
    int deleteHead() {
        if(!stack1.empty()) {
            int a = stack1.top();
            stack1.pop();
            return a; 
        } 
        return -1;
    }
};
```

# 方案二

1. 添加元素直接添加； 
2. 删除元素时判断第二个栈是不是空，是的话一次性将第一个栈元素全部压入，再删除就可以了
3. 删除时如果第二个栈不空，那直接弹出就可以了。

```C++
class CQueue {
public:
    stack<int> s1;
    stack<int> s2;
    CQueue() {
    }
    void appendTail(int value) {
        s1.push(value);
    }
    
    int deleteHead() {
        if(s1.empty() && s2.empty()) {
            return -1;
        }
        while(!s1.empty()){
            s2.push(s1.top());
            s1.pop();
        }
        int res = s2.top();
        s2.pop();
        return  res;

    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```

* 插入元素：
    * 时间复杂度：O(1)
        判断元素个数和删除队列头部元素都使用常数时间。
        复杂度。
    * 空间复杂度：O(1)
        从第一个栈弹出一个元素，使用常数空间。
* 删除元素：
    * 时间复杂度：O(n)
        插入元素时，对于已有元素，每个元素都要弹出栈两次，压入栈两次，因此是线性时间
    * 空间复杂度：O(n)
        需要使用额外的空间存储已有元素。