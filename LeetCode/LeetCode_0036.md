# LeetCode_0036 有效的数独

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。



# 解答

```C++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        /*
        * 先检查行是否存在，再检查列，最后检查3x3
        */
        unordered_map<int,int>hashMap;
        //1.先检查行
        for(int i = 0;i < 9;i++) {
            hashMap.clear();
            for(int j = 0;j < 9;j++) {
                if(board[i][j] == '.') continue;
                hashMap[board[i][j]]++;
                if(hashMap[board[i][j]] > 1) return false;
            }
        }
        //2.再检查列
        for(int i = 0;i < 9;i++) {
            hashMap.clear();
            for(int j = 0;j < 9;j++) {
                if(board[j][i] == '.') continue;
                hashMap[board[j][i]]++;
                if(hashMap[board[j][i]] > 1) return false;
            }
        }
        //3.再检查3x3
        for(int i = 0; i < 3; i++){
            for(int j = 0; j < 3; j++){
                int i_index = i * 3,j_index = j*3;
                hashMap.clear();
                for(int si=0; si<3; si++){
                    for(int sj=0; sj<3; sj++){
                        if(board[si + i_index][sj + j_index]=='.') continue;
                        hashMap[board[si + i_index][sj + j_index]]++;
                        if(hashMap[board[si + i_index][sj + j_index]] > 1) return false;
                    }
                }
            }
        }
        return true;
    }
};
```

* 时间复杂度：O(1)。只有 81 个元素。
* 空间复杂度：O(1)。