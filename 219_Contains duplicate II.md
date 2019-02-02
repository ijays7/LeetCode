## Contains Duplicate II

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j* in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3
Output: true
```

## Solution

这道题是 217 的加强版，判断数组中某两个值相等并且其索引之差的绝对值最大为 k。

这道题用了 HashMap 来做，其 key，value 分别存储数组中的值和索引，当判断 map 中已经存在了相同的 key 的时候，再进行 索引之差的判断，如果小于等于3，那么直接返回 true。 

因为 HashMap 插入和查询的时间复杂度为 O(1)，数组中每个元素需要遍历一次，所以总的时间复杂度为 O(n)。

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return false;
        }

        Map<Integer, Integer> maps = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (maps.containsKey(nums[i])) {
                if (Math.abs(i - maps.get(nums[i])) <= k) {
                    return true;
                }
            }
            maps.put(nums[i], i);
        }


        return false;
    }
```

