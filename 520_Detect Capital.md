## Detect Capital

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

1. All letters in this word are capitals, like "USA".
2. All letters in this word are not capitals, like "leetcode".
3. Only the first letter in this word is capital if it has more than one letter, like "Google".

Otherwise, we define that this word doesn't use capitals in a right way.

## Solution

这道题是给定一个字符串，判断该字符串是否符合题目中给出的大小写规则，即：

1. 要么全部大写
2. 要么全部小写
3. 要么仅首字母大写

这么我们直接暴力破解，首先将字符串全部转换为大写，如果前后字符串一致，那么肯定满足规则；同理，将字符串全部转换为小写，判断前后是否一致。最麻烦的首字母大写的情况，需要首先判断首字母是否大写，如果大写了，需要对余下字符串再进行一次全部转小写判断的操作。整体思路还是很流畅的。

```java
 public boolean detectCapitalUse(String word) {
        if (word == null || word.isEmpty()) {
            return false;
        }
        String allCaps = word.toUpperCase();
        if (allCaps.equals(word)) {
            return true;
        }

        String allLowercase = word.toLowerCase();
        if (allLowercase.equals(word)) {

            return true;
        }

        char firstLetter = word.charAt(0);
        if (firstLetter >= 65 && firstLetter < 97) {
            //大写
            if (word.length() > 1) {
                String str = word.substring(1);
                String lowercase = str.toLowerCase();

                return lowercase.equals(str);
            }
        }


        return false;
    }
```

