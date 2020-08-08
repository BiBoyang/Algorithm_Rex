# LeetCode_0599 两个列表的最小索引总和

假设Andy和Doris想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

你需要帮助他们用最少的索引和找出他们共同喜爱的餐厅。 如果答案不止一个，则输出所有答案并且不考虑顺序。 你可以假设总是存在一个答案。

示例 1:

```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
输出: ["Shogun"]
解释: 他们唯一共同喜爱的餐厅是“Shogun”。
```
示例 2:

```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
输出: ["Shogun"]
解释: 他们共同喜爱且具有最小索引和的餐厅是“Shogun”，它有最小的索引和1(0+1)。
```
**提示:**

1. 两个列表的长度范围都在 [1, 1000]内。
2. 两个列表中的字符串的长度将在[1，30]的范围内。
3. 下标从0开始，到列表的长度减1。
4. 两个列表都没有重复的元素。



# 解答
```C++
class Solution {
public:
    vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
        vector<string> res;
        //最小的索引和
        int MinIndexs = INT_MAX;
        unordered_map<string,int> hashMap;
        for(int i = 0;i<list1.size();i++) {
            hashMap[list1[i]] = i;
        }
        for(int i = 0;i < list2.size();i++) {
            //判断是否存在
            if(hashMap.count(list2[i])) {
                //索引和
                int index =  hashMap[list2[i]] + i;
                if(MinIndexs > index) {
                    MinIndexs = index;
                    res.clear();
                    res.push_back(list2[i]);
                } else if (MinIndexs == index) {
                    res.push_back(list2[i]);
                }
            }   
        }
        return res;
    }
};
```

* 时间复杂度：O(l1 + l2)。
* 空间复杂度：O(l1 * x)。其中 x 是字符串的平均长度。 