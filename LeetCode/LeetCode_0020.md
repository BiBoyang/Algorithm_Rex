
# LeetCode_0020 有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：
* 左括号必须用相同类型的右括号闭合。
* 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

# 解答

使用栈，利用先进先出的特点.
因此借助栈，一定要注意边界。
例如空字符串，奇数个符号的情况，不用进入循环，直接返回
入栈时，先判断，碰到一对满足的括号，例如（）{} ，就弹出；不满足就入栈，空栈也入栈
若最后栈为空，代表括号是有效的



```C++
class Solution {
public:
    bool isValid(string s) {
        stack<char> stringStack;
        for (int i = 0; i < s.length(); i++) {
            if (!stringStack.empty()) {
                if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
                    stringStack.push(s[i]);
                } else if (s[i] == ')') {
				    if (stringStack.top() == '(') {
					    stringStack.pop();
				    } else {
					    return false;
                    }
			    } else if (s[i] == ']') {
				    if (stringStack.top() == '[') {
					    stringStack.pop();
				    } else {
					    return false;
                    }
			    } else if (s[i] == '}') {
				    if (stringStack.top() == '{') {
					    stringStack.pop();
				    } else {
					    return false;
                    }
			    }
		    } else {
			    stringStack.push(s[i]);
		    }	
	    }
	    return stringStack.empty();
    }
};

```

复杂度分析
时间复杂度：O(n)，因为我们一次只遍历给定的字符串中的一个字符并在栈上进行 O(1) 的推入和弹出操作。
空间复杂度：O(n)，当我们将所有的开括号都推到栈上时以及在最糟糕的情况下，我们最终要把所有括号推到栈上。例如 ((((((((((。

