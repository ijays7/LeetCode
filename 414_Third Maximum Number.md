## Third Maximum Number

Given a **non-empty** array of integers, return the **third** maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).

**Example 1:**

```
Input: [3, 2, 1]

Output: 1

Explanation: The third maximum is 1.
```



**Example 2:**

```
Input: [1, 2]

Output: 2

Explanation: The third maximum does not exist, so the maximum (2) is returned instead.
```

## Solution

这道题是给定了一个非空的数组，返回数组中第三大的元素，如果不存在第三大的，那么就返回第其中最大的数。

### Approach1

很容易想到使用堆来做，维护一个大小为3的小顶堆，但需要注意的是，这道题里面可能不存在第三大的元素，我们还需要去判断一下最大的元素，并且数组中还有可能存在重复的元素，所以还需要在往 ProirityQueue 中添加数据时候判断已经添加。

因为遍历一遍数组需要 O(n) 的时间复杂度，PriorityQueue 的 offer() 和 poll() 的时间复杂度都是 O(logk)，所以总的时间复杂度为 O(n* logk)，其中 k 等于3。

```java
 public int thirdMax(int[] nums) {
        int largest = 0;
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(3);
        for (int n : nums) {
            largest = Math.max(largest, n);

            if (!priorityQueue.contains(n)) {
                priorityQueue.offer(n);
            }

            if (priorityQueue.size() > 3) {
                priorityQueue.poll();
            }
        }

        if (priorityQueue.size() < 3) {
            return largest;
        } else {
            return priorityQueue.peek();
        }
    }
```

### Approach2

因为题目中说最好可以使用 O(n) 的时间复杂度，所以上面的方法就不满足了。求第三大的数，其实我们就可以维护3个最大的数，分别为 max1，max2，max3，在每一次循环中，我们都去比较当前的值是否应该在前三个最大的数中，如果有比当前保存的值大，那么则替换到对应的位置上。

时间复杂度为 O(n)。

```java
  public int thirdMax(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        long max1 = Long.MIN_VALUE;
        long max2 = Long.MIN_VALUE;
        long max3 = Long.MIN_VALUE;

        for (int n : nums) {
            long value = (long) n;
            if (value > max1) {
                max3 = max2;
                max2 = max1;
                max1 = n;

            } else if (value > max2 && value != max1) {
                max3 = max2;
                max2 = n;
            } else if (value > max3 && value != max2 && value != max1) {
                max3 = n;
            }
        }
        return (int) (max3 == Long.MIN_VALUE ? max1 : max3);
  }
```



