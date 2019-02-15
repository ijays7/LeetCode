##  Merge Sorted Array

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n*respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution

题目中给定两个已经排好序的数组，要将 nums2 这个数组合并到 nums1 这个数组中，并且假设 nums1 数组中有足够的空间容纳两个数组的长度。

这道题目有一个前提，就是两个数组均是已经排好序的，所以我们处理起来就相对比较容易了。定义3个指示器，分别表示 nums1 合并之后的有效下标，当前 nums1 中有效下标，当前 nums2 中有效下标，从 nums1 合并之后的长度开始设置值，即比较两个数组最后有效位的大小，从后往前设置即可。

因为要遍历一次数组，所以整体的时间复杂度为 O(n)，n 表示 nums1 数组的长度。

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int totalIndex = m + n - 1;
        int numsIndex1 = m - 1;
        int numsIndex2 = n - 1;

        while (totalIndex >= 0) {
            if (numsIndex1 >= 0 && numsIndex2 >= 0) {
                if (nums1[numsIndex1] > nums2[numsIndex2]) {
                    nums1[totalIndex] = nums1[numsIndex1];
                    numsIndex1--;
                } else {
                    nums1[totalIndex] = nums2[numsIndex2];
                    numsIndex2--;
                }
            } else if (numsIndex1 >= 0) {

                nums1[totalIndex] = nums1[numsIndex1];
                numsIndex1--;

            } else if (numsIndex2 >= 0) {
                nums1[totalIndex] = nums2[numsIndex2];
                numsIndex2--;
            }

            totalIndex--;
        }
    }
```

