## Valid Anagram

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

## Solution

这道题的意思是判断有效的字母异位词。

这道题方法很多。第一种方法是采用先排序。分别按照字母序对字符串进行排序，然后比较排序过后的字符串是否相等。这样的话难点就是对字符串进行排序了，直接调用现成的方法，还是比较简单。时间复杂度为 O( N * logN )。

第二种方法是采用 map 这种数据结构。map 的 key，value 分别存储字符和该字符出现的次数。这里可以分别将两个字符串中出现的字母分别加到 map 中，然后比较两个 map 是否相同。这里还可以这样，先将一个字符串中的字母加入 map 中，然后第二个字符串遍历的时候判断该字符是否在 map 中，如果在 map 中且次数仅为1次，那么直接移除这个字母，否则将次数减1。

因为 Map 的插入和访问时间复杂度都是 O(1)，所以总的时间复杂度为 O(n)。

第一种方法（Kotlin）:

```kotlin
fun isAnagram(s: String, t: String): Boolean {

    val sArray = s.toCharArray()
    val tArray = t.toCharArray()
    sArray.sort()
    tArray.sort()
    val strS = String(sArray)
    val strT = String(tArray)
    return strS == strT
}
```

第二种方法（Java）：

```java
public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        Map<Character, Integer> map = new HashMap<>();

        for (Character c : s.toCharArray()) {
            if (map.containsKey(c)) {
                map.put(c, map.getOrDefault(c, 0) + 1);
            } else {
                map.put(c, 1);
            }
        }

        for (Character c : t.toCharArray()) {
            if (map.containsKey(c)) {
                int count = map.get(c);
                if (count == 1) {
                    map.remove(c);
                } else {
                    map.put(c, count - 1);
                }
            }
        }
        return map.isEmpty();
    }
```

