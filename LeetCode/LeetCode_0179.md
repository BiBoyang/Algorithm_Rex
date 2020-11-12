# LeetCode_0179 最大数

给定一组非负整数 nums，重新排列它们每位数字的顺序使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

 

示例 1：

```
输入：nums = [10,2]
输出："210"
```

示例 2：

```
输入：nums = [3,30,34,5,9]
输出："9534330"
```
示例 3：

```
输入：nums = [1]
输出："1"
```
示例 4：

```
输入：nums = [10]

输出："10"
```

提示：

* 1 <= nums.length <= 100
* 0 <= nums[i] <= 109





## 解答

```C++
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        int len = nums.size();
        vector<string>strNums(len);
        
        //1.转换成字符串数组
        for(int i=0;i<len;++i) {
            //首先将每个整型数转换为字符串,这个处理是为了防止数字超过标准
            strNums[i] = to_string(nums[i]);
        }
        
        // int len = nums.size();
        // vector<string> strNums(len);
        // for(int i=0;i<len;++i) {
        //     //首先将每个整型数转换为字符串,这个处理是为了防止数字超过标准
        //     strNums[i] = to_string(nums[i]);
        // }
        
        
        
        //2.排序
        sort(strNums.begin(),strNums.end(),[](string a,string b){
            return a + b > b + a;
        });
        //3.穿成一个字符串
        string ans = "";
        for(int i = 0;i< len;i++) {
            ans += strNums[i];
        }
        //4.特殊情况
        if(ans[0] == '0')
            return "0";
        return ans;
    }
};
```
