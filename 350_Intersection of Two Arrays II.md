## Intersection of Two Arrays II

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

## Solution

这道题是[Intersection of Two LinkedList](https://github.com/ijays7/LeetCode/blob/master/160_Intersection%20of%20Two%20Linked%20Lists.md)的升级版。给定了两个整形数组，要求返回两个数组中的交叉部分。注意：交叉的部分需要全部返回，即便数字是重复的！

这道题最容易想到的思路是使用 list。将一个数组全部放入一个 list 中，接下来遍历另外一个数组，遇到有交叉的部分再放入另外一个 list 中。代码还是比较容易。

此算法的时间复杂度为 O(m+n)，m，n 分别表示两个数组的长度。

```kotlin
fun intersect(nums1: IntArray, nums2: IntArray): IntArray {
    if (nums1.isEmpty() || nums2.isEmpty()) {
        return intArrayOf()
    }
    val array1 = arrayListOf<Int>()
    val array2 = arrayListOf<Int>()

    nums1.forEach {
        array1.add(it)
    }

    nums2.forEach {
        if (array1.contains(it)) {
            array1.remove(it)
            array2.add(it)
        }
    }

    return array2.toIntArray()
}
```

