##  Maximum Product of Three Numbers

Given an integer array, find three numbers whose product is maximum and output the maximum product.

**Example 1:**

```
Input: [1,2,3]
Output: 6
```

 

**Example 2:**

```
Input: [1,2,3,4]
Output: 24
```

## Solution

这道题意思是给定一个整数数组，找到数组中的3个数乘积最大并将其输出。

首先我们很容易想到，要想乘积最大，只要分别最大一般乘积就是最大，所以我们将数组进行一次排序即可。只是这里面要主要为负数的情况，若只有一个负数则越负越大，两个负数则负负得正。所以我们需要判断下。

因为进行了一次排序，所以时间复杂度为 O( n*logn )，其中 n 表示数组的长度。

```java
 public int maximumProduct(int[] nums) {
        int length = nums.length;
        Arrays.sort(nums);

        int result = nums[length - 1] * nums[length - 2] * nums[length - 3];

        if (nums[1] < 0) {
            return Math.max(nums[0] * nums[1] * nums[length - 1], result);

        } else {
            return result;
        }

    }
```

### 优化

上面的方法会首先进行一次排序，因此时间复杂度为 O( n*logn)。在 leetcode 的 discussion 里面看到一个解法，使用空间换时间，采用 PriorityQueue 这种数据结构，记录数组中最大和最小的元素。因为数组中每个元素都要进队列一次，所以时间复杂度为 O(n)。

这里队列处理的比较巧妙，实例化了一个最小堆和一个最大堆，其中最大堆逆置了大小的顺序，然后再比较两个头元素的绝对值大小并将这个元素出队列，最后枚举出各种情况的结果并且比较得到最大的结果。

```java
public int maximumProduct(int[] nums) {
        
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(nums.length);
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(nums.length, Collections.reverseOrder());
        
        for(int i = 0; i < nums.length; i++) {
            minHeap.add(nums[i]);
            maxHeap.add(nums[i]);
        }
        
        int maxNum = (Math.abs(minHeap.peek()) > Math.abs(maxHeap.peek())) ? minHeap.poll() : maxHeap.poll();
        
        int mixPair = minHeap.peek() * maxHeap.peek() * maxNum;
        int negPair = minHeap.poll() * minHeap.poll() * maxNum;
        int posPair = maxHeap.poll() * maxHeap.poll() * maxNum;
        
        if(minHeap.size() > maxHeap.size()) return Math.max(negPair, posPair);

        return Math.max(negPair, mixPair);
    }
```

