## Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

## Solution

这道题是判断一个数是不是回文数，比如121，反过来还是121，所以是回文数。而-121反过来是121-，所以-121不是回文数。

### Approach1

第一种方法简单粗暴，直接把数字转化为字符串，然后 reverse 字符串，最后判断 reverse 之后的字符串与原字符串是否相同。

kotlin:

```kotlin
 fun isPalindrome(x: Int): Boolean {
        val strX = x.toString()
        if (strX.reversed() == strX) {
            return true
        }

        return false    
 }
```

Java:

```java
  public boolean isPalindrome(int x) {
        String toStr = String.valueOf(x);
        char[] charArrays = toStr.toCharArray();
        StringBuilder builder = new StringBuilder();
        for (int i = charArrays.length - 1; i >= 0; i--) {
            builder.append(charArrays[i]);
        }
        String reversed = builder.toString();
        if (reversed.equals(String.valueOf(x))) {
            return true;
        }
        return false;
    }
```



### Approach2

第二种方法是采用数学的方法。计算一个数字是否是回文数字，我们其实就是将这个数字除以10，保留它的余数，下次将余数乘以10，加上这个数字再除以10的余数。

需要注意：

1. 负数不是回文数字
2. 0是回文数字

时间复杂度为 O(logN)，N表示数字的长度。

```java
 public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        } else if (x == 0) {
            return true;
        } else {
            // x 是正数

            int tmp = x;
            int y = 0;

            while (x != 0) {
                y = y * 10 + x % 10;
                x = x / 10;
            }

            return tmp == y;

        }
    }
```





