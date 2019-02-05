## Remove Duplicates from Sorted Array

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

## Solution

这道题是给定一个排好序的数组，移除数组中重复的元素使得每个元素只出现一次并且返回数组最新的长度。题目中还有一个要求，不能重新分配数组，必须得空间复杂度为 O(1)。

这里我们可以直接遍历一次数组，用一个计数器 count 来表示不重复的元素个数。在每一次循环中，判断当前元素是否重复，如果重复就直接跳过，否则复制下一个值到当前来。

当然还有一种更简单的办法，遍历一次数组，将每个元素放入 set 中，最后返回 set 的大小。只是需要分配一个 set 的内存空间，不符合题目要求。

使用第一种方法的时间复杂度为 O(n)，n 为数组的长度。

```kotlin
fun removeDuplicates(nums: IntArray): Int {
    if (nums.isEmpty()) {
        return 0
    }
    if (nums.size == 1) {
        return 1
    }

    var count = 0

    for (i in 1 until nums.size) {
        if (nums[count] != nums[i]) {
            count++
            nums[count] = nums[i]
        }
    }

    return count + 1

}
```



