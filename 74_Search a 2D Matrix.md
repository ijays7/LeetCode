## Search a 2D Matrix

> 此题来自 LeetCode 第74题：[Search a 2D Matrix](https://leetcode-cn.com/problems/search-a-2d-matrix/)

编写一个算法来判断`m*n`的矩阵中，是否存在一个目标值。其中矩阵满足：

- 每行中的整数从左到右按升序排列
- 每行中的第一个整数大于前一行的最后一个整数

示例：

> 输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
>
> 输出：true

## Solution1

这道题拿到的第一想法是切入矩阵的右上角。从条件中可知，每一行的最后1位都是该行的最大值，那么我们只需拿`target`和每一行的的最后一位进行比较就能确认`target`是否在该行中，如果确认`target`可能存在于该行，那么再进行二分查找即可。整体思路还是比较简单直接。

```kotlin
fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {
    var row = 0
    while (row < matrix.size) {
        var left = 0
        var right = matrix[row].lastIndex
        when {
            target < matrix[row][right] -> {
                // 在范围内
                while (left <= right) {
                    val mid = (left + right) / 2
                    when {
                        matrix[row][mid] == target -> {
                            return true
                        }
                        matrix[row][mid] > target -> {
                            right = mid - 1
                        }
                        else -> {
                            left = mid + 1
                        }
                    }
                }
                row++
            }
            target == matrix[row][right] -> {
                return true
            }
            else -> {
                row++
            }
        }

    }
    return false
}
```



## Solution2

上面的做法虽然能够通过，但是表现并不好，在 LeetCode 上只超过了9%的 Kotlin 提交，说明上面的思路还有很大的提升空间。

仔细分析上面的代码，首先通过每一行的末尾确定`target`所在的行，然后再对该行进行二分查找，包含了两层循环，总共的时间复杂度就是`O(m * lgn)`。

可以在草稿纸上把上面的矩阵画一下，可以如果把矩阵压平，即想象成一个`1 * (m * n)`的矩阵，那么题目是不是就相当于是判断一个有序的数组中是否包含`target`了呢？这不就是典型的二分查找题目了吗？所以，顺着这个思路，我们就可以写出仅需要一层二分查找的代码了。

不过这二分查找的代码怎么写呢？头尾都好说，中间值怎么确定呢？利用题目中的有序，我们就可以确定中间所在的行，所在的列，即`mn/2/m`和`(mn/2)%m`。在纸上一画便知。那么我们优化过的代码就可以完成了。总共的时间复杂度为`O(lg(mn-1))`。果然提交之后运行时间为180ms，比之前好了很多。

```kotlin
fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {
    val row = matrix.size
    if (row == 0) return false

    val column = matrix[0].size
    if (column == 0) return false

    var start = 0
    var end = row * column - 1
    var mid = 0
    var midValue = 0
    while (start <= end) {
        mid = (start + end) / 2
      // 确定二分查找的中间值
        midValue = matrix[mid / column][mid % column]

        when {
            midValue == target -> {
                return true
            }
            midValue > target -> {
                end = mid - 1
            }
            else -> {
                start = mid + 1
            }
        }
    }

    return false
}
```

