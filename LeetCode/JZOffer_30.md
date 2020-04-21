# 面试题30. 包含min函数的栈

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

示例:
```C++
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

# 解答
使用辅助栈。

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
```