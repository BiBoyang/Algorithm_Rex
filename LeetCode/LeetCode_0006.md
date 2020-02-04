
# LeetCode_0006 Z 字形变换


将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：

L   C   I   R
E T O E S I I G
E   D   H   N

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：

string convert(string s, int numRows);


## 解答
按行排序。

```C++
class Solution {
public:
	string convert(string s, int numRows) {
		if (numRows == 1) return s;
		vector<string> rows(min(numRows, int(s.size()))); // 防止s的长度小于行数
		int curRow = 0;
		bool goingDown = false;
		for (char c : s) {
			rows[curRow] += c;
            // 当前行curRow为0或numRows -1时，箭头发生反向转折
			if (curRow == 0 || curRow == numRows - 1) {
				goingDown = !goingDown;
			}
			curRow += goingDown ? 1 : -1;
		}
		string ret;
        // 从上到下遍历行
		for (string row : rows) {
			ret += row;
		}
		return ret;
	}
};
```

复杂度：
时间复杂度：O(n)，其中 n==len(s)
空间复杂度：O(n)
