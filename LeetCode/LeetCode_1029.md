# LeetCode_1029 两地调度
公司计划面试 2N 人。第 i 人飞往 A 市的费用为 costs[i][0]，飞往 B 市的费用为 costs[i][1]。

返回将每个人都飞到某座城市的最低费用，要求每个城市都有 N 人抵达。

 

示例：

输入：[[10,20],[30,200],[400,50],[30,20]]
输出：110
解释：
第一个人去 A 市，费用为 10。
第二个人去 A 市，费用为 30。
第三个人去 B 市，费用为 50。
第四个人去 B 市，费用为 20。

最低总费用为 10 + 30 + 50 + 20 = 110，每个城市都有一半的人在面试。

## 解答
使用贪心算法
```
class Solution {
public:
    int twoCitySchedCost(vector<vector<int>>& costs) {
        int res = 0;
        //让差值从大到小排列
        sort( costs.begin(), costs.end(), [](vector<int> a, vector<int> b){
            return a[0] - a[1] > b[0] - b[1];
        });
        //做前后双指针，前一半去b，后一半去a
        for( int i = 0, j = costs.size()-1; i < j; i++, j--) {
            res += costs[i][1] + costs[j][0];
        }
        return res;
    }
};
```