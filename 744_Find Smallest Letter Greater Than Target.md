## Find Smallest Letter Greater Than Target

Given a list of sorted characters `letters` containing only lowercase letters, and given a target letter `target`, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is `target = 'z'` and `letters = ['a', 'b']`, the answer is `'a'`.

**Examples:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"
```

## Solution

这道题是给定了一个有序的字符数组，仅包含小写字母，要求在数组中找到一个比给定 target 大的数中最小的那个。这是典型的二分查找使用场景。

时间复杂度为 O(logN)。

```java
 public char nextGreatestLetter(char[] letters, char target) {

        int low = 0;
        int high = letters.length - 1;

        while (low <= high) {
            int mid = (low + high) / 2;
            if (letters[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return letters[low % letters.length];
    }
```

