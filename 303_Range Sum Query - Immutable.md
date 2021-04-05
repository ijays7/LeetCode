## Range Sum Query - Immutable

Given an integer array `nums`, find the sum of the elements between indices `left` and `right` inclusive, where `(left <= right)`.

Implement the `NumArray` class:

- `NumArray(int[] nums)` initializes the object with the integer array `nums`.
- `int sumRange(int left, int right)` returns the sum of the elements of the `nums` array in the range `[left, right]` inclusive (i.e., `sum(nums[left], nums[left + 1], ... , nums[right])`).

## Solution

这道题拿到的第一个想法是 Brutal force，直击了当，代码如下：

```kotlin
class NumArray(private val nums: IntArray) {

    fun sumRange(left: Int, right: Int): Int {
        if (left < 0 || right >= nums.size)return 0

        var sum = 0
        var index = left
        while (index <= right){
            sum += nums[index]
            index++
        }
        return sum

    }
}
```

上面的代码没什么好说的，一目了然，然而提交后傻眼了，执行用时632ms，超过了37%的 Kotlin 提交。显而易见上面的代码有很大的提升空间。

分析一下上面的代码，每次在计算的时候都会进行遍历求和，时间复杂度为 O(m - n + 1)，所以当 sumRange 函数多次执行时，执行用时就会变得愈发的长。因此为了降低总的执行时间，需要降低 sumRange 函数的时间复杂度。我们通过分析题目，可以得出当 `i <= j`时，`sumRang(i,j)）`可以写成：
$$
\begin{align}
\\&setRange(i,j)\\&=\sum_{k=i}^j nums[k]\\&=\sum_{k=0}^j nums[k] - \sum_{k=0}^{i-1}nums[k]
\end{align}
$$
所以要计算`setRange(i,j)`，需要分别计算`nums`数组中下标 0 到`j`的和和下标 0 到`i - 1`的和，并且计算两者的差值，这样做有什么好处呢？我们可以在初始化方法中，首先计算出各个下标的前缀和，将其缓存起来，这样在`setRange`函数调用的时候直接读取然后求差即可，这样在计算的时候就实现了 O(1) 的时间复杂度。

具体实现代码如下，其中初始化`sum`数组时时间复杂度为 O(n)，`setRange`函数执行时时间复杂度为 O(1)。

```kotlin
class NumArray(nums: IntArray) {
    private val sum = IntArray(nums.size + 1)

    init{
        sum[0] = 0
        for(i in nums.indices){
            sum[i+1] = sum[i] + nums[i]
        }
    }

    fun sumRange(left: Int, right: Int): Int {
        // if (left < 0 || right >= nums.size)return 0

        return sum[right + 1] - sum[left]
    }
}
```

