## Contains Duplicate

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1:**

```
Input: [1,2,3,1]
Output: true
```

## Solution

这道题是判断一个数组中是否有重复的元素，如果存在，就返回true。最简单的当然是暴力破解，循环硬解。这里我做的是使用 Set 集合这种数据结构，因为 Set 中不允许重复元素，所以将数组中每个元素放入 Set 中，然后比较数组和 Set 大小是否相等。

因为 Set 插入和查询的时间复杂度都是 O(1) 的，但是每个元素必须循环一次，所以总的时间复杂度为 O( n )。

```java
  public boolean containsDuplicate(int[] nums) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        Set<Integer> set = new HashSet<>();
        for (Integer value : nums) {
            set.add(value);
        }


        return set.size() != nums.length;
    }
```

这道题还有升级版 219_Contains Duplicate II