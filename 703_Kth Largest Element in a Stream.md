## Kth Largest Element in a Stream

Design a class to find the **k**th largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Your `KthLargest` class will have a constructor which accepts an integer `k`and an integer array `nums`, which contains initial elements from the stream. For each call to the method `KthLargest.add`, return the element representing the kth largest element in the stream.

**Example:**

```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

## Solution

这道题是返回流式数据中第 k 大的元素，要求设计一个类，构造函数中接收整数 k 和一个整形数组，即为第 k 大的元素，调用 `KthLargest.add`，返回第 k 大的元素。

返回数据中第 k 大的元素，第一种方式可以是保存前 k 个最大的数，即我们首先对数组中数据进行一次排序，再记录前 k 个最大的元素，如果新来的数据比第 k 个最大中的最小都小的话，直接跳过这个元素，如果新来的数据比前 k 个最大中最小的大，则直接替换这个元素。这个方法的瓶颈在于先对数组进行排序，时间复杂度为 O( N*KlogK )，其中 K 为最大的元素个数。

第二种方式就是使用优先队列，求前 K 个最大的元素实质上就是维护一个大小为 k 的小顶堆，新来的元素只要比堆定的元素小则直接跳过，如果大于堆顶元素则将堆顶元素踢出，将新元素加入堆中，自动产生新的堆顶。优先队列中得到堆顶元素和删除堆顶都是 O(1)，产生新的堆顶是 O(logK)，所以总的时间复杂度为 O(N*logK)，比第一种方式快了不少。

```java
class KthLargest {
    private int k;

    private PriorityQueue<Integer> priorityQueue;

    public KthLargest(int k, int[] nums) {
        this.k = k;

        priorityQueue = new PriorityQueue<>(k);
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        if (priorityQueue.size() < k) {
            priorityQueue.offer(val);
        } else if (priorityQueue.peek() < val) {
            priorityQueue.poll();
            priorityQueue.offer(val);
        }


        return priorityQueue.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```

