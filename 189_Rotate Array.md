## Rotate Array

Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.

**Example 1:**

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

## Solution

```java
 public void rotate(int[] nums, int k) {
        int[] rotated = new int[nums.length];
        System.arraycopy(nums, 0, rotated, 0, rotated.length);

        for (int i = 0; i < nums.length; i++) {
            int position = (i + k) % nums.length;
            nums[position] = rotated[i];
        }
    }
}
```

