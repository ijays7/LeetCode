## Kth Largest Element in an Array

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solution

这道题给定了一个没有排序的数组，需要找到数组中第 k 大的元素。

### Sort

首先最容易想到的方法是先对数组进行排序，然后直接找到第 k 大的元素。下面的代码直接调用了库函数进行排序，有作弊嫌疑，但是能够通过 leetcode，算一种方法吧。时间复杂度为 O(n*logn)。

```java
 public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        Arrays.sort(nums);

        return nums[k - 1];
    }
```

### PriorityQueue

第二种方法想到的是使用 PriorityQueue 这种数据结构。题目中要求第 k 大的元素，实际上可以变成我们我们维护一个大小为 k 的小顶堆，第 k 大的元素就在堆顶。同时我们遍历数组，只要发现比堆顶更大的元素，就将现在的堆顶踢掉，把当前元素加入堆中，直到最后还在堆顶的元素就是我们的结果。

使用 PriorityQueue 的插入和删除时间复杂度都是 O(logn)，因此总的时间复杂度为 O(n*logk)。

```java
 public int findKthLargest(int[] nums, int k) {

        if (nums == null || nums.length == 0) {
            return 0;
        }

        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(k);
        for (int i = 0; i < nums.length; i++) {
            if (i <= k - 1) {
                priorityQueue.offer(nums[i]);
            } else {
                if (priorityQueue.peek() < nums[i]) {
                    priorityQueue.poll();
                    priorityQueue.offer(nums[i]);
                }
            }
        }


        return priorityQueue.peek();
    }
```

上面的代码是我自己写的，当看了 discussion 的代码后，发现确实在 for 循环里面往 PriorityQueue 里面插入的代码写得有点冗余，可以直接往里面添加。

```java
 for (int value : nums) {
            priorityQueue.offer(value);

            if (priorityQueue.size() > k) {
                priorityQueue.poll();
            }
    }
```



