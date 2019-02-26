## Intersection of Two Arrays

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

## Solution

这道题是计算两个给定数组的交叉部分。我们直接用 HashSet 来处理。

时间复杂度为 O(n)，空间复杂度为 O(n)。

```java
public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return new int[]{};
        }
        Set<Integer> set = new HashSet<>();
        for (int n : nums1) {
            set.add(n);
        }

        List<Integer> result = new ArrayList<>();
        for (int n : nums2) {
            if (set.remove(n)) {
                result.add(n);
            }
        }

        if (result.size() != 0) {
            int[] arrays = new int[result.size()];
            for (int i = 0; i < result.size(); i++) {
                arrays[i] = result.get(i);
            }
            return arrays;
        }

        return new int[]{};

    }
```

