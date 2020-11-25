# LeetCode_252 会议室
给定一个会议时间安排的数组 intervals ，每个会议时间都会包括开始和结束的时间 intervals[i] = [starti, endi] ，请你判断一个人是否能够参加这里面的全部会议。

 

示例 1：
```
输入：intervals = [[0,30],[5,10],[15,20]]
输出：false
```

示例 2：
```
输入：intervals = [[7,10],[2,4]]
输出：true
```

# 解答

按开始时间进行排序，然后在比较开始时间和结束时间。

```C++
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end(),[](vector<int> A,vector<int> B) {
            return A[0] < B[0];
        });
        
        for(int i = 1;i < intervals.size();i++){
            if(intervals[i][0] < intervals[i - 1][1]){
                return false;
            }
        }
        return true;
    }
};
```

* 时间复杂度：O(n * n)
* 空间复杂度：O(1)