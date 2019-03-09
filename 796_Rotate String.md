## Rotate String

We are given two strings, `A` and `B`.

A *shift on A* consists of taking string `A` and moving the leftmost character to the rightmost position. For example, if `A = 'abcde'`, then it will be `'bcdea'` after one shift on `A`. Return `True` if and only if `A` can become `B` after some number of shifts on `A`.

```
Example 1:
Input: A = 'abcde', B = 'cdeab'
Output: true
```

## Solution

这道题是给定了两个字符串 A，B。对字符串 A 进行移位操作，如果 A 移位之后能够得到字符串 B，那么就返回 true，否则返回 false。

一开始我拿到这道题首先想到的就是类似于移位密码，对每个字符进行移位操作，如果越界了就进行取模操作，我想这道题思路也是类似，问题就是如果确定移位的大小，即移动字符几位。想到的方法是以 A 的最后一位字符为基准，查找该字符在 B 的位置，然后计算移动了多少位，但是后来在经过几次 wrong answer 之后，发现要准确定位移动的位数代价颇大，遂放弃。

换了另外一种方法，只要是经过移位的话，那么所有的情况一定在 A + A 中（可以在纸上验证一下），所以我们只需要保证 B 包含于 A + A 即可。当然别忘了验证 A 和 B 的长度，防止 A = a，B = aa 的情况 。

时间复杂度为 O($N^2$)，N 表示字符串 A 的长度，空间复杂为 O(N)。

```java
  public boolean rotateString(String A, String B) {
        if (A == null || B == null){
            return false;
        }
      // 这些操作可以省略
        if (A.length() == 0 && B.length() == 0){
            return true;
        }else if (A.length() == 0){
            return false;
        }else if (B.length() == 0){
            return false;
        }
        return A.length() == B.length() && (A + A).contains(B);
    }
```

