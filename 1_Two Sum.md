## Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```



### MySolution

这道题是返回数组中数值相加等于给定值的位置组合，思路还是比较简单，常见的方法有两种：第一种就是直接干，Brutal force，两个 for 循环遍历，暴力计算两个数之和等于 target，时间复杂度为 O( $n^2​$ )；第二种方式更有一点技巧，目的是计算 **a + b = target** ，第一种方法我们也是直接按加法计算，我们也可以按减法算，给定一个 a，去计算 **b = target - a**，即寻找这个 b 所在的位置。

方法一：

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2]; 
        for(int i = 0;i < nums.length;i++){
            for(int j = i+1;j < nums.length;j++){
                if(nums[i]+nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                    break;
                }
            }
        }
        return result;
    }
}
```



方法二：

```kotlin
class Solution {
 fun twoSum(nums: IntArray, target: Int): IntArray {
    val map = HashMap<Int, Int>()
    for ((index, value) in nums.withIndex()) {
        if (map.containsKey(target - value)) {
            return intArrayOf(index, map[target - value]!!)
        }

        map[value] = index
    }

    return intArrayOf()
 }

}
```

这是用 Kotlin 写的代码，用一个 HashMap 存储差值和位置的关系映射，只用遍历数组一次，因此时间复杂度为 O(n)，较第一种方式更优。

