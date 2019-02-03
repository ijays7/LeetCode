## Most Common Word

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

 

**Example:**

```
Input: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```

## Solution

这道题是给定了一个字符串，一个名叫 banned 的字符串数组，需要统计出字符串中出现次数最多的单词并且这个单词不在 banned 数组中。

我的思路是先将字符串全部转换为小写，并且将字符串按照标点符号份组成字符串数组，接下来遍历数组，用一个 map 保存单词出现的次数，然后 map 中剔除被禁止的单词，即 banned 中的内容，最后统计 map 中 value 值最大的 key。

时间复杂度为 O(n)。

```java
  public static String mostCommonWord(String paragraph, String[] banned) {
        if (paragraph == null || paragraph.length() == 0) {
            return "";
        }

        String[] splitedArray = paragraph.toLowerCase().split("[ !?',;.]+");

        Map<String, Integer> map = new HashMap<>();

        for (String s : splitedArray) {
            map.put(s, map.getOrDefault(s, 0) + 1);
        }

        for (String ban : banned) {
            map.remove(ban);
        }
        String result = null;

        for (String s : map.keySet()) {
            if (result == null || map.get(s) > map.get(result)) {
                result = s;
            }
        }


        return result;
    }
```

