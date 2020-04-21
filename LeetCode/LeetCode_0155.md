#  LeetCode_0155 最小栈

设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

    push(x) —— 将元素 x 推入栈中。
    pop() —— 删除栈顶的元素。
    top() —— 获取栈顶元素。
    getMin() —— 检索栈中的最小元素。

示例:
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

# 解答

辅助栈和数据栈同步

编码简单，不用考虑一些边界情况，就有一点不好：辅助栈可能会存一些“不必要”的元素。

```C++
class MinStack {
public:
    /** initialize your data structure here. */
    stack<int> dataStack;
    stack<int> minStack;

    MinStack() {

    }

    void push(int x) {
        dataStack.push(x);
        if(minStack.size() == 0) {
            minStack.push(x);
        } else {
            if(x < minStack.top()){
                minStack.push(x);
            } else {
                minStack.push(minStack.top());
            }
        }
    }
    
    void pop() {
        if(dataStack.size() == 0) {
            return ;
        }
        dataStack.pop();
        minStack.pop();
    }
    
    int top() {
        return dataStack.top();
    }
    
    int min() {
        return minStack.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
```
