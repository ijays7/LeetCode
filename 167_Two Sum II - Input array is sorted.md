## Two Sum II - Input array is sorted

Given an array of integers that is already ***sorted in ascending order\***, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

### Solution

这道题是 [Two Sum](https://github.com/ijays7/LeetCode/blob/master/1_Two%20Sum.md) 的升级版，把给定的整型数组改为了已经排好序的整型数组，输出还是一样，返回数组两个元素之和等于 target 的小标组成的数组，这里还规定，返回的数组必须是升序。

这里我们可以使用两个指针 start，end，一个指向数组的头部，一个指向数组的尾部，计算头尾之和。如果相加之和刚好等于 target，那么 start 和 end 就是我们需要寻找的两个元素，否则，就使用从两头往中间夹的方式寻找，直到 start 和 end 相等为止。最后，不要忘了给返回的 start，end 分别加1。

代码使用 Kotlin 提交：

```kotlin
fun twoSum(numbers: IntArray, target: Int): IntArray {
    if (numbers.isEmpty()) {
        return intArrayOf()
    }

    var start = 0
    var end = numbers.lastIndex
    var hasResult = false

    println("start-->$start--end-->$end")

    while (start < end) {
        val sum = numbers[start] + numbers[end]
        if (sum < target) {
            start++
        } else if (sum > target) {
            end--
        } else {
            hasResult = true
            break
        }
    }

    if (hasResult) {
        start += 1
        end += 1
        return intArrayOf(start, end)
    }
    return intArrayOf()
}
```

