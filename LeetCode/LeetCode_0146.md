# LeetCode_0146. LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。



# 解答

```C++
class LRUCache {
    private:
    int cap;
    //创建双向链表list,内部配对存储pair数据
    list<pair<int,int>>cacheList;
    unordered_map<int,list<pair<int,int>>::iterator>hashMap;
    
    public:
    LRUCache(int capacity):cap(capacity){
        
    };
    // O(1)
    int get(int key) {
        // 判断it是否存在hashmap中
        auto it = hashMap.find(key);
        if(it == hashMap.end()){
            return -1;
        }
        //将cacheList里的value的数据重新插入到cacheList.beigin()之前中
        cacheList.splice(cacheList.begin(),cacheList,it->second);
        return it->second->second;
    }
    // O(1)
    void put(int key, int value) {
        // 判断it是否存在hashmap中
        auto it = hashMap.find(key);
        //如果it存在
        if(it != hashMap.end()) {
            cacheList.erase(it->second);
        }
        //头部插入key、value
        cacheList.push_front(make_pair(key,value));
        //key改为对应cacheList头部
        hashMap[key] = cacheList.begin();
        if(int(hashMap.size()) > cap) {
            //找出cacheList的最后一个元素的key
            int k = cacheList.rbegin()->first;
            cacheList.pop_back();
            hashMap.erase(k);
        }
    }     
};
```