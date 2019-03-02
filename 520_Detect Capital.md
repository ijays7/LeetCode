## Detect Capital

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

1. All letters in this word are capitals, like "USA".
2. All letters in this word are not capitals, like "leetcode".
3. Only the first letter in this word is capital if it has more than one letter, like "Google".

Otherwise, we define that this word doesn't use capitals in a right way.

## Solution

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

