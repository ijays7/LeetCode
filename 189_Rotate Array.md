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

这道题是给定一个数组，每个元素移动 k 位，返回移动过后的数组。

下面的方法是我看到题的第一反应的方法。即遍历整个数组，每个元素移动 k 位，那么移动过后的位置就应该是   (i+k) % nums.length ，其中 i 为当前的位置。因为直接对 nums 里面的元素赋值了，所以需要先将 nums 进行 copy 一遍，再进行遍历操作。

时间复杂度为 O( n )。当然其实题目里面还有一个 hint，说尽量用多的方法来做这道题，并且满足 O(1)的时间复杂度，显然这种做法就不行了。

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

