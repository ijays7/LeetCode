## Majority Element

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

## Solution

这道题的意思是给定一个非空数组，需要找到数组中出现次数最多的数，其出现次数大于了 n/2。题目中已经假定数组中一定存在这个数。

这道题首先的思路就是暴力破解，两重 for 循环，时间复杂度为 O($N^2$)。

另外一种常见的思路就是使用 Map 来计数。将数组中所有元素放入 Map 中，直接遍历 Map，找到出现次数最多的那个元素。HashMap 中放入元素和取出元素的时间复杂度都是 O(1)，所以总的时间复杂度为 O(N)，N 表示数组的长度。

```java
 public int majorityElement(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int times = 0;
        int majorityElement = 0;
        Map<Integer, Integer> map = new HashMap<>();

        for (int n : nums) {
            map.put(n, map.getOrDefault(n, 0) + 1);
        }
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() > times) {
                times = entry.getValue();
                majorityElement = entry.getKey();
            }
        }

        return majorityElement;
    }
```

