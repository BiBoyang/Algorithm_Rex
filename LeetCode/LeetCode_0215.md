# LeetCode_0215  数组中的第K个最大元素
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5

示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4

说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。
## 解答
#### 方法一：直接使用堆
直接使用最大堆，时间复杂度为nlogn
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        
        priority_queue<int, vector<int>, less<int>>heap(nums.begin(),nums.end());
        for(int i = 0;i< k-1;i++) {
            heap.pop();
        }
        return heap.top();   
    }
};
```
直接使用最小堆，时间复杂度为nlogk
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        
        priority_queue<int, vector<int>, greater<int> >heap;
        for(int i=0;i < nums.size();i++) {
            if(heap.size() == k) {
                int x = heap.top();
                if(nums[i] > x) {
                    heap.pop();
                    heap.push(nums[i]);
                }
            } else {
                    heap.push(nums[i]);
            }
        }
        return heap.top();   
    }
};
```

#### 方法二：制作一个优先队列
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
    
        int len = nums.size();
        int temp;
        for(int i=nums.size()/2-1;i>=0;i--)
            buildHeap(nums,i,len);
        for(int i=len-1;i>=len-k;i--) {
            temp = nums[0];
            nums[0] = nums[i];
            nums[i] = temp;
            buildHeap(nums,0,i);
        }
        return temp;
    }
    void buildHeap(vector<int>&nums,int i,int len) {
        int childIndex;
        int temp;
        while(2*i+1<len) {
            temp = nums[i];
            childIndex = 2*i+1;
            if(childIndex < len-1 && nums[childIndex] < nums[childIndex+1])
                childIndex++;
            if(nums[childIndex] > temp) {
                nums[i] = nums[childIndex];
                nums[childIndex] = temp;
                i = childIndex;
            } else {
                break;
            }
        }
    }  
};
```

#### 方法三：快速排序

```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return findKthLargest(nums, 0, nums.size()-1 , k - 1 );
    }
private:
    int findKthLargest( vector<int>& nums, int l, int r, int k ){
        if( l == r ) {
            return nums[l];
        }
        int p = partition( nums, l, r );
        if( p == k ) {
            return nums[p];
        } else if( k < p ) {
            return findKthLargest( nums, l, p-1, k);
        } else {// k > p
            return findKthLargest( nums, p+1 , r, k );
        }
    }
    int partition( vector<int>& nums, int l, int r ){
        int p = rand() % (r-l+1) + l;
        swap( nums[l] , nums[p] );
        int lt = l + 1; //[l+1...lt) > p ; [lt..i) < p
        for( int i = l + 1 ; i <= r ; i ++ ) {
            if( nums[i] > nums[l]) {
                swap(nums[i], nums[lt++]);
            }
        }
        swap(nums[l], nums[lt-1]);
        return lt-1;
    }    
};
```