## Reverse String

Write a function that takes a string as input and returns the string reversed.

**Example:**
Given s = "hello", return "olleh".



方法一：

此方法是最只直觉的做法。将传进来的字符串转换为字符数组，然后遍历此数组将其倒序输出。虽然直觉上很好理解，但是却不是最优的方法。此方法时间复杂度为O(n)。

``` java
public class Solution {
    public String reverseString(String s) {
        char[] output = new char[s.length()];
        char[] str = s.toCharArray();
        for (int i = str.length; i >0; i--) {
            output[str.length-i] = str[i-1];
        }
        return  String.valueOf(output);
    }
}
```



方法二：

这个方法非常讨巧，直接调用了JDK中StringBuffer类的reverse方法。

``` java
public class Solution {
    public String reverseString(String s) {
     return new StringBuffer(s).reverse().toString();
    }
}
```









