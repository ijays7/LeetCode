## LRUCache

Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**
Could you do both operations in **O(1)** time complexity?

## Solution

### Approach1

这道题是让我们设计实现一个 LRUCache 类，需要支持 get 和 put 方法，且时间复杂度为 O(1)。

我们知道，LRUCache 算法指的是最近最少使用。当缓存空间满了的时候，将最近最少使用的元素从缓存中删除。缓存中维护了一个双向链表，当链表中空间足够且不包含即将放入的元素时候，直接将该元素放在头节点；当链表空间足够且包含即将放入的元素的时候，我们移除掉已经在链表中的那个元素，并且将该元素放入头节点。

在Java 中，LinkedHashMap 是HashMap 的子类，其内部使用了双向链表，这道题使用LinkedHashMap 是相当取巧的做法。

因为HashMap 的access 和 delete 都是O(1) 的时间复杂度，因此总的时间复杂度为 O(1)。

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

### Approach2

第二种方法是我在[Youtube](https://www.youtube.com/watch?v=S6IfqDXWa10)上看到的，这种方法内部使用了一个HashMap，并且自己维护了一个双向链表，相比于第一种取巧的实现，第二种方法应该才是真正在面试的时候面试官想问的。

```java
import java.util.HashMap;
import java.util.Map;

public class LRUCache2 {

    private Map<Integer, DNode> map = new HashMap<>();
    private DNode head, tail;
    private int totalItemInCache;
    private int maxCapacity;

    public LRUCache2(int maxCapacity) {
        totalItemInCache = 0;
        this.maxCapacity = maxCapacity;

        // 初始化双向链表
        head = new DNode();
        head.prev = null;

        tail = new DNode();
        tail.next = null;

        head.next = tail;
        tail.prev = head;
    }

    /**
     * @param key
     * @return
     */
    public int get(int key) {
        DNode node = map.get(key);
        boolean isItemInCache = node != null;

        if (isItemInCache) {
            // 如果在缓存列表中，放入头部
            moveToHead(node);
            return node.value;
        }
        return -1;
    }

    /**
     * @param key
     * @param value
     */
    public void put(int key, int value) {
        DNode node = map.get(key);
        boolean isItemInCache = node != null;

        if (isItemInCache) {
            // 如果Item已经存在
            node.value = value;
            moveToHead(node);

        } else {
            node = new DNode();
            node.value = value;
            node.key = key;

            // 将节点放入hashMap中
            map.put(key, node);
            addNode(node);

            totalItemInCache++;

            // 如果超过了缓存的最大值,则移除最老的元素
            if (totalItemInCache > maxCapacity) {
                removeLRUCacheFromStructure();

            }
        }
    }

    private void removeLRUCacheFromStructure() {

        DNode tail = popTail();
        map.remove(tail.key);
        totalItemInCache--;
    }

    private DNode popTail() {
        DNode itemBeingRemoved = tail.prev;
        removeNode(itemBeingRemoved);
        return itemBeingRemoved;
    }

    private void moveToHead(DNode node) {
        removeNode(node);
        addNode(node);
    }

    private void removeNode(DNode node) {
        DNode preNode = node.prev;
        DNode nextNode = node.next;

        // 移除双向链表指针
        preNode.next = nextNode;
        nextNode.prev = preNode;
    }

    /**
     * 添加节点
     *
     * @param node
     */
    private void addNode(DNode node) {
        node.prev = head;
        node.next = head.next;

        head.next.prev = node;
        head.next = node;

    }

    /**
     * Definition of doubly linked list node
     */
    class DNode {
        int key;
        int value;
        DNode prev;
        DNode next;
    }
}
```

