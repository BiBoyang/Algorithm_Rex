# LeetCode_0605 种花问题

假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 n 。能否在不打破种植规则的情况下种入 n 朵花？能则返回True，不能则返回False。

示例 1:
```
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```
示例 2:
```
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```


# 解答

在数组的两端各添加一个0；然后查找有多少个0的左右两边也是0。

```C++
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int count = 0;
        flowerbed.insert(flowerbed.begin(),0);
        flowerbed.insert(flowerbed.end(),0);
        for(int i = 1;i < flowerbed.size() - 1;i++){
            if(flowerbed[i - 1] == 0 && flowerbed[i] == 0 && flowerbed[i + 1] == 0) {
                flowerbed[i] = 1;
                count++;
            }
        }
        if(n <= count) {
            return true;
        } else {
            return false;
        }
    }
};
```

* 时间复杂度：O(n)
* 空间复杂度；O(1)