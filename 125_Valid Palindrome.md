## Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**

```
Input: "race a car"
Output: false
```



## Solution

这道题意思是给定一个字符串，判断它是不是回文。题目中要求只考虑字符串中字母和数字的部分，并且忽略大小写。

判断回文的解题思路很容易想到双指针法。即使用头尾指针循环字符串，当遇到两个字符串不等等时，即认为不是回文。但从题目的示例中来看，字符串中还包含标点符号等其他字符，所以还以为将这一部分刨除。

#### Code 1

```kotlin
fun isPalindrome(s: String): Boolean {
    if (s.isBlank()) return true
  // 如果字符串为空或者长度为1，都认为是回文
    if (s.length == 1) return true

    var start = 0
    var end = s.lastIndex

    while (start <= end) {
        while (start < end && !isAlphaNumeric(s[start])) {
            start++
        }

        while (start < end && !isAlphaNumeric(s[end])) {
            end--
        }

        if (s[start].toLowerCase() != s[end].toLowerCase()) {
          // 记得忽略大小写
            return false
        }

        start++
        end--
    }

    return true
}

private fun isAlphaNumeric(c: Char): Boolean {
    return c.isLetter() || c.isDigit()
}
```



#### Code2

上面的代码很简单，也很容易想到，但是并没有用到太多Kotlin 的特性，下面的解法是参考LeetCode 上的网友的Kotlin 写法，使用Kotlin 的扩展方法，直接将字符串进行分割，大大提高了代码的可读性。

```kotlin
fun isPalindrome(s: String): Boolean {
    // 这里的partition 函数是将字符串按字母和数字的方式分割字符串，返回的其实是一个Pair<String,String>,
   // 满足条件的字符串即first 为Pair 的第一个参数，不满足条件的的字符串second 为Pair 的第二个参数。
    val letters = s.partition {
        it.isLetter() || it.isDigit()
    }.first.toLowerCase()

    var left = 0
    var right = letters.lastIndex
    while (left < right) {
        if (letters[left] != letters[right]) {
            return false
        } else {
            left++
            right--
        }
    }

    return true
}

```

这里的两种方式其实追根结底是一种方法，时间复杂度都是O(n)。

