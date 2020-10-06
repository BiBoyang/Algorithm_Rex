# LeetCode_1013 总持续时间可被 60 整除的歌曲

在歌曲列表中，第 i 首歌曲的持续时间为 time[i] 秒。

返回其总持续时间（以秒为单位）可被 60 整除的歌曲对的数量。形式上，我们希望索引的数字  i < j 且有 (time[i] + time[j]) % 60 == 0。

 

示例 1：
```
输入：[30,20,150,100,40]
输出：3
解释：这三对的总持续时间可被 60 整数：
(time[0] = 30, time[2] = 150): 总持续时间 180
(time[1] = 20, time[3] = 100): 总持续时间 120
(time[1] = 20, time[4] = 40): 总持续时间 60
```
示例 2：
```
输入：[60,60,60]
输出：3
解释：所有三对的总持续时间都是 120，可以被 60 整数。
```

提示：
* 1 <= time.length <= 60000
* 1 <= time[i] <= 500

# 解答
## 解法一
刚开始想用暴力的方法来解决，但是发现 超出时间限制了。
我就要换一种思路。
```
class Solution {
public:
  int numPairsDivisibleBy60(vector<int>& time) {
      // 初始化一个大小为60的数组
      vector<int> nums(60);  
      int ans = 0;  
      for(int i = 0;i< time.size();i++) {
          //对当前第i个元素除以60取余
          int j = time[i] % 60;
          ans = ans + nums[(60 - j) % 60];
          nums[j]++; 
      }
      return ans;
  }
};
```

## 解法二
我们使用两数之和的方法。先对每个元素取余，然后将取余之后的结果加入到hashMap中，hashMap[i]表示取余结果为i的个数，我们需要找出对应的60-i的去进行匹配。
这里要注意0和30这两个特殊的点。同时由于为了避免重复，我们在筛选的时候实际上只需要对前余数小于等于30的数进行计算，因为每个元素都可以找到一个对应的60-i。
注意：[A,B]和[B,A]是
```
class Solution {
public:
  int numPairsDivisibleBy60(vector<int>& time) {
      //创建一个hashMap
      unordered_map<int, int>hashMap;
      int ans = 0;
      //将取余的元素加入hashmap中
      for (int i = 0; i < time.size(); i++)
          hashMap[time[i] % 60]++;
      //对预期为0的计算
      if (hashMap[0])	
          /*
          * 这里我们需要明白hashmap中的0取余的结果，
          * 实际上这些都是60为结尾的。而且这些排列组合中实际
            上会有调换顺序的两种结果，所以我们要对结果除以2
          */
          ans += hashMap[0] * (hashMap[0] - 1) / 2;
      
      for (int i = 1; i < 30; i++) {
          if (hashMap[i] && hashMap[60 - i])
              ans += hashMap[i] * hashMap[60 - i];
      }
      //对取余为30的计算，道理和上边一样
      if (hashMap[30])	
          ans += hashMap[30] * (hashMap[30] - 1) / 2;
      return ans;
  }
};

```

