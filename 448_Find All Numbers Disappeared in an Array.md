## Find All Numbers Disappeared in an Array

Given an array of integers where 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear twice and others appear once.

Find all the elements of [1, *n*] inclusive that do not appear in this array.

Could you do it without extra space and in O(*n*) runtime? You may assume the returned list does not count as extra space.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

## Solution

这道题意思是给定一个整形数组，并且数组中元素范围为1到 n（n 为数组的长度），其中有些元素出现了不止一次，需要找到其中确实的数字。

这道题如果是常规思路的话，就很容易了，直接放到一个 HashSet 中，遍历整个数组，遇到数组中的元素就从 HashSet 中删除。整个算法时间复杂度为 O(n)，空间复杂度为 O(n)。

```java
 public List<Integer> findDisappearedNumbers(int[] nums) {
     if (nums == null && nums.length == 0){
            return null;
        }
        Set<Integer> set = new HashSet<>();
        List<Integer> result = new ArrayList<>();
        for (int i = 1;i <= nums.length;i++){
            set.add(i);
        }

        for (int n:nums){
            set.remove(n);
        }

        Iterator iterator = set.iterator();
        while (iterator.hasNext()){
    
           result.add((Integer)iterator.next());
        }

        return result;      
    }
```

