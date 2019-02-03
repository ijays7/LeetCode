## Implement strStr()

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

## Solution

这道题是返回在字符串 haystack 中特定的字符串首先出现的位置，也有多种方法，可以直接调 indexOf()，也可以循环查找。时间复杂度为 O(n)。

```java
 public int strStr(String haystack, String needle) {

        if (haystack.length() == 0 && needle.length() == 0) {
            return 0;
        }
        if (needle.length() == 0) {
            return 0;
        }

        char[] strArray = haystack.toCharArray();
        for (int i = 0; i < strArray.length; i++) {
            if (strArray[i] == needle.charAt(0)) {

                if (strArray.length - i < needle.length()) {
                    return -1;
                }

                String subs = haystack.substring(i, i + needle.length());

                if (needle.equals(subs)) {
                    return i;
                }
            }
        }

        return -1;
    }
```

两年前的做法，比较暴力，只比16%的 Java 提交好。

```java
 public int strStr(String haystack, String needle) {
        if(haystack == null || needle ==null ){
            return -1;
        }
        
       int start = 0;
        // 如果剩下的字母不够needle长度就停止遍历
        while(start <= haystack.length() - needle.length()){
            int i1 = start, i2 = 0;
            while(i2 < needle.length() && haystack.charAt(i1)==needle.charAt(i2)){
                i1++;
                i2++;
            }
            if(i2 == needle.length()) return start;
            start++;
        }
        return -1;
    }
```

