## First Unique Character in a String

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.
```

## Solution

这道题是给定一个字符串，找到第一个不重复的字母并且返回它的下标。如果不存在，就返回-1。

我一看到这道题，思路比较直接。首先遍历一遍字符串，将字符映射到一个哈希表中，记录每个字母出现的次数。有了映射之后，再遍历一遍字符串，在哈希表中找到第一个出现次数为1的那个字符。

我把这个算法写完之后，心想这个结果应该不会太好，因为遍历了两遍字符串，使用一个 HashMap 来存储字符和出现次数的映射关系，整体的时间复杂度为 O(n)+O(n)，总的时间复杂度为O (n)。

```java
   public int firstUniqChar(String s) {
        if (s == null || s.length() == 0) {
            return -1;
        }
        int result = -1;
        Map<Character, Integer> map = new HashMap<>();
        for (Character c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        for (int i = 0; i < s.length(); i++) {
            if (1 == map.get(s.charAt(i))) {
                result = i;
                break;
            }
        }

        return result;
    }

```

这里参考了一下 discussion 里面的解法，漏掉了题目中的一个条件，字符串中仅包含小写，所以可以遍历26个英文字母，判断每个字母第一次出现的下标和最后一次出现的下标是否一致，最后取最小的满足条件的下标即可。

```java
   public int firstUniqChar(String s) {
        if (s == null || s.length() == 0) {
            return -1;
        }
        int result = Integer.MAX_VALUE;
        for (int i = 'a'; i <= 'z'; i++) {
            int id = s.indexOf(i);
            if (id != -1 && id == s.lastIndexOf(i)) {

                result = Math.min(result, id);
            }
        }


        return result == Integer.MAX_VALUE ? -1 : result;
    }
```

