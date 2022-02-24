# LeetCode_0502. IPO

假设 力扣（LeetCode）即将开始 IPO 。为了以更高的价格将股票卖给风险投资公司，力扣 希望在 IPO 之前开展一些项目以增加其资本。 由于资源有限，它只能在 IPO 之前完成最多 k 个不同的项目。帮助 力扣 设计完成最多 k 个不同项目后得到最大总资本的方式。

给你 n 个项目。对于每个项目 i ，它都有一个纯利润 profits[i] ，和启动该项目需要的最小资本 capital[i] 。

最初，你的资本为 w 。当你完成一个项目时，你将获得纯利润，且利润将被添加到你的总资本中。

总而言之，从给定项目中选择 最多 k 个不同项目的列表，以 最大化最终资本 ，并输出最终可获得的最多资本。

答案保证在 32 位有符号整数范围内。

 
示例 1：
```
输入：k = 2, w = 0, profits = [1,2,3], capital = [0,1,1]
输出：4
解释：
由于你的初始资本为 0，你仅可以从 0 号项目开始。
在完成后，你将获得 1 的利润，你的总资本将变为 1。
此时你可以选择开始 1 号或 2 号项目。
由于你最多可以选择两个项目，所以你需要完成 2 号项目以获得最大的资本。
因此，输出最后最大化的资本，为 0 + 1 + 3 = 4。
```

示例 2：
```
输入：k = 3, w = 0, profits = [1,2,3], capital = [0,1,2]
输出：6
```

# 解答

1. 只能选择 k 次，所以要选择 k 次最大的利润。
2. 将所需要的资本从小到大排序，从所有小于手头资本的项目中，找到最大的利润项目 j；然后 手头资本变成 w + profits[j]，继续从可以的项目中购入；

```
typedef pair<int, int> pii;
class Solution {    
public:
    int findMaximizedCapital(int k, int w, vector<int>& profits, vector<int>& capital) {
        int len = profits.size();
        int cur = 0;
        //  创建最大堆
        priority_queue<int , vector<int>, less<int>> que;
        vector<pii> arr;
        //加入数组，按照资本在前，得利在后的顺序，方便排序
        for(int i = 0;i < len;i++) {
            arr.push_back({capital[i],profits[i]});
        }
        sort(arr.begin(),arr.end());

        for(int i = 0;i < k;i++){
            //小心得利数量越界 && 本钱要够
            while(cur < len && arr[cur].first <= w){
                que.push(arr[cur].second);
                cur++;
            }
            if(!que.empty()){
                w += que.top();
                que.pop();
            }

        }
        return w;
    }
};
```