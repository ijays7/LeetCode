## Single Number

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

## Solution

这道题意思是给定一个非空的整形数组，数组中只有一个数字出现了1次，其他每个数字都出现了2次，需要找到那个出现一次的数字。

首先想到的解法是遍历一遍数组，将每个数字放到一个 list 中，如果 list 里面已经存在了这个数字，那么就把它从 list 中删除，最后我们返回 list 中的那个数字。

这个解法时间复杂度是 O($n^2$)，因为遍历一遍数组需要 O(n) 的时间复杂度，而 list 的 contains 其实也是 for 循环，所以总的时间复杂度是 O($n^2$)。

```java
 public int singleNumber(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for (int n : nums) {
        
            if (list.contains(n)) {
                list.remove(new Integer(n));
            }else{
                list.add(new Integer(n));
            }
        }
        return list.get(0);
    }
```

这道题用上面的这种方法在面试的时候估计多半会遭，因为 O($n^2$) 的时间复杂度不是太令人满意。这道题真正的考点是位操作。

复习一下，xor 是异或操作，如果参与运算的两个位相同，则返回0，否则返回1，即 0 xor 0 = 0，0 xor 1 = 1，1 xor 0 = 1，1 xor 1 = 0，并且，

***0 异或任何数等于任何数***

***1 异或任何数等于任何数取反***

```kotlin
fun singleNumber(nums: IntArray): Int {
    var result = 0
    nums.forEach {
        result = result.xor(it)
    }
    return result
}
```



