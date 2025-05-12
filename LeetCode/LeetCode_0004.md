# LeetCode_0004 寻找两个有序数组的中位数

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。
请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

```
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

示例 2:

```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

# 解答

```C++
class Solution {
public:
	double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
		int n = nums1.size();
		int m = nums2.size();

		if (n > m) {
			return findMedianSortedArrays(nums2, nums1);
		}

		// Ci 为第i个数组的割,比如C1为2时表示第1个数组只有2个元素。LMaxi为第i个数组割后的左元素。RMini为第i个数组割后的右元素。
		int LMax1, LMax2, RMin1, RMin2, mid1, mid2, Left = 0, Right = 2 * n;  //我们目前是虚拟加了'#'所以数组1是2*n长度

		while (Left <= Right) {
			mid1 = (Left + Right) / 2;  //mid1是二分的结果
			mid2 = m + n - mid1;
            
            if(mid1 == 0) {
                LMax1 = INT_MIN;
            } else {
                LMax1 = nums1[(mid1-1) / 2];
            }
            
            if(mid1 == 2 * n) {
                RMin1 = INT_MAX;
            } else {
                RMin1 = nums1[mid1 /2];
            }
            
            if(mid2 == 0) {
                LMax2 = INT_MIN;
            } else {
                LMax2 = nums2[(mid2 -1) / 2];
            }
            
            if(mid2 == 2 * m) {
                RMin2 = INT_MAX;
            } else {
                RMin2 = nums2[mid2 / 2];
            }
            
			if (LMax1 > RMin2) {
				Right = mid1 - 1;
            } else if (LMax2 > RMin1) {
				Left = mid1 + 1;
            } else {
                return (max(LMax1, LMax2) + min(RMin1, RMin2)) / 2.0;
            }
				
		}
		return -1;
	}
};
```

