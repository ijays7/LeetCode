## LRUCache

Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**
Could you do both operations in **O(1)** time complexity?

## Solution

这道题是让我们设计实现一个 LRUCache 类，需要支持 get 和 put 方法，且时间复杂度为 O(1)。

我们知道，LRUCache 算法指的是最近最少使用。当缓存空间满了的时候，将最近最少使用的元素从缓存中删除。缓存中维护了一个双向链表，当链表中空间足够且不包含即将放入的元素时候，直接将该元素放在头节点；当链表空间足够且饱含即将放入的元素的时候，我们移除掉已经在链表中的那个元素，并且将该元素放入头节点。

在Java 中，LinkedHashMap 是HashMap 的子类，其内部使用了双向链表，这道题使用LinkedHashMap 是相当取巧的做法。

```java
class LRUCache {
    private Map<Integer, Integer> map;

    public LRUCache(int capacity) {
        // 使用 LinkedHashMap，构造方法中传入true 表示按照访问顺序迭代，false 表示按照插入顺序迭代
        map = new LinkedHashMap<Integer, Integer>(capacity, 0.75f, true) {
            @Override
            // 重写removeEldestEntry，实现LRUCache 的过期机制，即当size 大于cache 的size 时候自动删   除最近最少使用的元素
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > capacity;
            }
        };

    }

    public int get(int key) {
        return map.getOrDefault(key, -1);
    }

    public void put(int key, int value) {
        if (map.get(key) != null) {
            map.remove(key);
        }
        map.put(key, value);

    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

