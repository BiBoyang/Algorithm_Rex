# LeetCode_0705 设计哈希集合
不使用任何内建的哈希表库设计一个哈希集合

具体地说，你的设计应该包含以下的功能

* `add(value)`：向哈希集合中插入一个值。
* `contains(value)` ：返回哈希集合中是否存在这个值。
* `remove(value)`：将给定值从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。

示例:
```C++
MyHashSet hashSet = new MyHashSet();
hashSet.add(1);         
hashSet.add(2);         
hashSet.contains(1);    // 返回 true
hashSet.contains(3);    // 返回 false (未找到)
hashSet.add(2);          
hashSet.contains(2);    // 返回 true
hashSet.remove(2);          
hashSet.contains(2);    // 返回  false (已经被删除)
```

注意：

* 所有的值都在 [0, 1000000]的范围内。
* 操作的总数目在[1, 10000]范围内。
* 不要使用内建的哈希集合库。

# 解答

```C++
class MyHashSet {
public:    
    vector<list<int>> arr;
    /** Initialize your data structure here. */
    MyHashSet() {
        arr.resize(10001);
    }
    
    void add(int key) {
        int index = key % arr.size();
        if(contains(key)) return ;
        else arr[index].push_back(key);
    }
    
    void remove(int key) {
        int index = key % arr.size();
        auto ite = arr[index].begin();
        for(; ite != arr[index].end(); ite++){
            if((*ite) == key) 
                break;
        }
        if(ite != arr[index].end())
            arr[index].erase(ite);
    }
    
    /** Returns true if this set contains the specified element */
    bool contains(int key) {
        int index = key % arr.size();
        auto ite = arr[index].begin();
        for(; ite != arr[index].end(); ite++){
            if((*ite) == key) 
                break;
        }
        return ite!=arr[index].end();
    }
};

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet* obj = new MyHashSet();
 * obj->add(key);
 * obj->remove(key);
 * bool param_3 = obj->contains(key);
 */
```