## Sliding Window Maximum

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

## Solution

这道题是输出滑动窗口的最大值。给定一个数组，有一个长度为 k 的滑动窗口，每次向右移动一位，输出每次窗口中的最大值。

### 使用PriorityQueue

我们很容易想到使用优先队列这种数据结构，维护一个长度为 k 的堆，堆顶表示每次的最大值，每次移动窗口，就将滑动窗口中最左边的元素删除，并将新加入窗口的元素加入队列，每次记录堆顶的元素即可。

```java
  public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }

        int[] result = new int[nums.length - k + 1];
        // 大顶堆
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(k, Collections.reverseOrder());
        for (int i = 0; i < k; i++) {
            priorityQueue.offer(nums[i]);
        }

        result[0] = priorityQueue.peek();

        for (int i = k; i < nums.length; i++) {
            priorityQueue.remove(nums[i - k]);
            priorityQueue.offer(nums[i]);
            result[i + 1 - k] = priorityQueue.peek();
        }

        return result;
    }
```



