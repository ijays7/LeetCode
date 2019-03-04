## Reverse Only Letters

Given a string `S`, return the "reversed" string where all characters that are not a letter stay in the same place, and all letters reverse their positions.

**Example 1:**

```
Input: "ab-cd"
Output: "dc-ba"
```

## Solution

这道题意思是给定一个字符串，仅对字母进行逆置操作，比如 “ab-cd”，经过变换变成 “dc-ba”。

这道题我一开始思路走偏了，想通过遍历字符串数组，进行移位操作，不过这个操作中要对非字母符号进行太多判断，较为麻烦。后来放弃了。

后来采用的是两个指针的方法。一个指针指向开头，一个指针指向结尾。遍历整个字符串数组，分别移动两个指针，进行换位操作，遇到非字母的字符直接跳过即可。

这个方法非常巧妙，从两边往中间扫描，不过其实我们也做过不少这种类型的题了，应该迅速反应出来的。

整体的时间复杂度为 O(n)，空间复杂度为 O(1)。

```java
public String reverseOnlyLetters(String S){
        if (S == null || S.length() == 0){
            return "";
        }

        int start = 0;
        int end = S.length() - 1;
        char[] strs = S.toCharArray();
        while (start < end){
            while (start < end && !Character.isLetter(strs[start])){
                start++;
            }
            while (start < end && !Character.isLetter(strs[end])){
                end--;
            }
            swap(strs,start++,end--);
        }

        return new String(strs);
    }

    private void swap(char[] strs, int start, int end){
        char temp = strs[start];
        strs[start] = strs[end];
        strs[end] = temp;
    }
```

