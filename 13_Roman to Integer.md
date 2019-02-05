## Roman to Integer

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

**Example 1:**

```
Input: "III"
Output: 3
```

## Solution

这道题是将罗马数字转换为整数。每个罗马数字表示特定的整数，当它们组合表示的时候，可以表示不同的整数，这道题保证了输入的大小为1到3999。

这道题其实思路还是比较直接，我们用一个 map 来存储罗马数字表示的规则，遍历需要转换的字符串数组，理论上直接将每个字母锁表示的值加起来即可。但是，题目中说到了有一个规则，比如 I 在 V 的前面就不是 5+1 而是 5-1了，5，50，500类似，这里当时我做的时候就是直接枚举了以上的所有情况，比较复杂。

这样做的时间复杂度为 O(n)，n 表示字符串的长度。

```java
  public int romanToInt(String s) {
         Map<String, String> map = new HashMap<>(8);
        map.put("I", "1");
        map.put("V", "5");
        map.put("X", "10");
        map.put("L", "50");
        map.put("C", "100");
        map.put("D", "500");
        map.put("M", "1000");

        char[] array = s.toCharArray();
        int count = 0;
        for (int i = 0; i < array.length; i++) {
            int value = Integer.parseInt(map.get(String.valueOf(array[i])));
            if (i + 1 < array.length) {
                int valueNext = Integer.parseInt(map.get(String.valueOf(array[i + 1])));
                if ((valueNext % 5 == 0 && value % 5 != 0) || ((valueNext % 500 == 0) && value % 500 != 0)
                        || ((valueNext % 50 == 0) && value % 50 != 0)) {
                    value = 0 - value;
                }

            }
            count = value + count;

        }
        return count;
    }
```

