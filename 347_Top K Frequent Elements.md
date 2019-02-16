## Top K Frequent Elements

Given a non-empty array of integers, return the **k** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

## Solution

这道题是给定了一个非空的整型数组，返回其中出现第 k 频繁的元素。

到目前为止，已经做过不少 top K 的问题了，其中大部分都可以使用堆来解决，这道题也是一样。

最容易想到的思路，遍历一遍数组，用一个 HashMap 存储元素与其出现次数的映射，接下来遍历这个 HashMap，同时我们维护一个 大小为 k 大的小顶堆，也就是我们的 PriorityQueue。最后将 PriorityQueue 中元素输出到一个 List 中即可。这里需要注意，由于使用的是小顶堆，如果直接往 List 中添加的话，输出的结果就会是升序的，所以我们需要添加的时候指定顺序或者对 List 进行一次 reverse 操作。

我们来分析一下算法的时间复杂度，首先进行遍历一次数组时间复杂度是 O(N)，PriorityQueue 的插入是 O(logK)，所以总的时间复杂度为 O(N+NlogK) 也就是 O(NlogK)。

```java
  public static List<Integer> topKFrequent(int[] nums, int k) {

        Map<Integer, Integer> map = new HashMap<>(nums.length);
        PriorityQueue<Map.Entry<Integer, Integer>> priorityQueue = new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());

        for (int number : nums) {
            map.put(number, map.getOrDefault(number, 0) + 1);
        }

        List<Integer> list = new LinkedList<>();

        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            priorityQueue.offer(entry);
            if (priorityQueue.size() > k) {
                priorityQueue.poll();
            }
        }
        while (!priorityQueue.isEmpty()) {
            list.add(0, priorityQueue.poll().getKey());
        }

        return list;
    }
```

注意：最后指定输出 List 顺序的时候可以使用 LinkedList。我一开始使用的是 ArrayList，Leetcode 上运行时间为 76 ms。后来注意到调用 add 方法的时候是制定添加到第 0 位，ArrayList 是数组实现的，这就涉及到要移动数组中之前的所有元素，是 O(n) 的时间复杂度，我们可以使用链表结构，插入是他的天然优势，只需要 O(1) 即可。换成 LinkedList 之后，运行时间一下减少到了 52 ms。所以，正确的使用数据结构是多么重要！