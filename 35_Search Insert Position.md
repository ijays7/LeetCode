## Search Insert Position

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example 1:**

```
Input: [1,3,5,6], 5
Output: 2
```

## Solution

这道题是给定一个排好序的数组，找出值 targe 在数组中所在的位置，如果数组中没有这个 target，那么返回这个 targe 应该所在的位置。

最简单的办法，Brutal Force。遍历数组，找出 target 所在位置的索引，如果没有找到，则与下一个值进行比较，直到找到满足条件的元素。

暴力破解的时间复杂度为 O( n )。  

Brutal Force:

```java
 public int searchInsert(int[] nums, int target) {
        if (nums[nums.length - 1] < target) {
            return nums.length;
        }
        if (nums[0] > target) {
            return 0;
        }

        for (int i = 0; i < nums.length; i++) {
            if (target == nums[i]) {
                return i;
            }
            int next = i + 1;
            if (next <= nums.length - 1) {
                if (nums[i] < target && nums[next] > target) {
                    return i+1;
                }
            }
        }

        return 0;
    }
```

当我们再来分析题目，这已经是一个排好序的数组，要找到数组中的target，仔细回想……这不就是二分查找的最佳使用场景吗？所以我们二分查找走一波。

使用二分查找的时间复杂度为 O(log N)

```kotlin
fun searchInsert(nums: IntArray, target: Int): Int {

    var low = 0
    var high = nums.size - 1

    while (low <= high) {
        val mid = (low + high) / 2
        if (nums[mid] == target) {
            return mid
        }
        if (nums[mid] > target) {
            high -= 1
        } else {
            low += 1
        }
    }
    
    return low
}
```

