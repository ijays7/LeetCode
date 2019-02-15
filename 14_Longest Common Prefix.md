## Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

## Solution

这道题意思是给定一个字符串数组，要求写一个方法返回数组中数组中最长的相同前缀。

首先我们想一下，如果存在相同的前缀，那么这个前缀只有可能存在于数组中长度最短的那个字符串中！有了这个概念之后，我们就可以使用暴力破解的方法了。两层 for 循环遍历，最外层为长度最短的字符串长度，里层根据外面的指示器 i 来直接判断当前字符是否相同，如果相同，则将其记录下来；如果不同，直接将记录的结果返回。

下面的方法有一个取巧的地方，不去显示的判断最短的字符长度，直接以第一个字符串的长度为基准，在第二层循环中判断如果当前的字符长度已经小于了外层指示器的长度时候，其实就可以认定没有相同的前缀了，直接返回结果即可。

这里的时间复杂度为 O(m*n)，其中 m 表示字符串数组的长度，n 表示数组中最短的字符串长度。

```java
 public String longestCommonPrefix(String[] strs) {

        if (strs == null || strs.length == 0) {
            return "";
        }
        if (strs.length == 1) {
            return strs[0];
        }

        StringBuilder builder = new StringBuilder();

        for (int i = 0; i < strs[0].length(); i++) {
            char character = strs[0].charAt(i);

            for (int j = 1; j < strs.length; j++) {
                if (i >= strs[j].length()) {
                    return builder.toString();
                }

                if (character != strs[j].charAt(i)) {
                    return builder.toString();
                }
            }

            builder.append(character);

        }

        return builder.toString();

    }
```

### Binary Search

这个解法是在 leetcode 中的 solution 上看到的，采用的是二分查找的思想。正如上文所说，如果存在相同的前缀，则必定存在于长度最短的字符串长度 minLength 中，我们就可以从起始位 low 开始到 minLength 查找，判断从 low 到 minLength 中间的元素是否相同。

这种方式会进行 logn 次 while 循环，每次循环进行 m*n 次比较，所以总的时间复杂度为 O（m * n *logn）。

 ```java
    public String longestCommonPrefix1(String[] strs) {

        if (strs == null || strs.length == 0) {
            return "";
        }
        if (strs.length == 1) {
            return strs[0];
        }

        int high = 0;
        int low = 1;
        for (String s : strs) {
            high = Math.min(high, s.length());
        }

        while (low <= high) {
            int mid = (low + high) / 2;

            if (isCommon(strs, mid)) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }


        return strs[0].substring(0, (low + high) / 2);

    }

    private boolean isCommon(String[] strs, int mid) {
        String sub = strs[0].substring(0, mid);
        for (String s : strs) {
            if (s.startsWith(sub)) {
                return true;
            }
        }

        return false;
    }
 ```

