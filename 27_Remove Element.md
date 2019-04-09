## Remove Element

Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example:**
Given input array *nums* = `[3,2,2,3]`, *val* = `3`

Your function should return length = 2, with the first two elements of *nums* being 2.



### My Solution

这道题是给定一个整形数组和一个 val，要求返回数组中移除所有 val 后的长度，并且不能开辟新的空间。

首先第一种思路是使用快慢指针，快指针循环整个数组，当发现当前值与 val 相等时，就跳过该值；当前值与 val 不想等时，则复制 nums[index] 到 nums[count] 中，并同时增加两个指针的值。

此算法时间复杂度为 O(N)。 

``` java
public class Solution {
    public int removeElement(int[] nums, int val) {
        if(nums.length==0){
            return 0;
        }
        int count = 0;
        for(int index = 0;index < nums.length;index++){
            if(nums[index]!= val){
                nums[count] = nums[index];
                count++;
            }
        }
        return repeat;
    }
}
```





