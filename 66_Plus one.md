

## Plus one

Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1:**

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

## Solution

这道题是考的数组。题目是给定一个非空的由非负数组成的数组，现在要求给数组表示的数加1，并且数组中都只能是单个数字。

刚好是看到这道题我以为很简单，直接取到数组最后一位数字然后加1就完事了。很高兴，呃……

如果是 [ 9 ] 这种情况，直接加 1 的话就是10，与题目不符合。那再判断一下吧，如果最后一位加1大于9就在数组中复制一遍数组，并且新增一位，最后一位是0。很高兴，呃……

冷静下来仔细想想，如果是 [ 9,9 ] 这种情况，需要进位两次，因此需要一个 for 循环来遍历这个数组，因为是从最后一位开始加1，所以从数组的尾部开始往前遍历，每一趟循环中判断当前数字加1后是否需要进位（大于9），最后遍历结束后后还需要进位的话，那么就需要给数组扩容。这里有一个很讨巧的地方，如果数组需要扩容的话，那么除了数组第一位为1，其余数字都为0。哈哈，上代码。

```kotlin
fun plusOne(digits: IntArray): IntArray {

    if (digits.isEmpty()) {
        return intArrayOf()
    }

    var needPlus = true

    for (i in digits.size - 1 downTo 0 step 1) {
        // 从尾部开始遍历

        var temp = digits[i]

        if (needPlus) {
            temp++
        }

        if (temp > 9) {
            needPlus = true
            digits[i] = 0
        } else {
            needPlus = false
            digits[i] = temp
        }
    }


    return if (needPlus) {
        val extendedResult = IntArray(digits.size + 1, { _ -> 0 })
        extendedResult[0] = 1
        extendedResult

    } else {
        digits
    }
}
```

