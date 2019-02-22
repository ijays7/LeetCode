## Keyboard Row

Given a List of words, return the words that can be typed using letters of **alphabet** on only one row's of American keyboard like the image below.

![](https://assets.leetcode.com/uploads/2018/10/12/keyboard.png)

**Example:**

```
Input: ["Hello", "Alaska", "Dad", "Peace"]
Output: ["Alaska", "Dad"]
```

## Solution

这道题是给定一串文字，要求返回在美式键盘中能中一行打出来的文字。

### Approach1

这道题我刚一看到思路比较直接，将每一行的文字与行数关系映射到一个 HashMap 中，然后遍历字符串列表，判断每个字符串的每个字符的行数位置是不是在同一行。虽然比较麻烦，但却是可行。

这个算法首先需要遍历一遍字符串列表，需要 O(m) 的时间复杂度，m 为列表长度，并且还需要遍历每个字符，所以总的时间复杂度为 O(m*n)，n表示每个字符的长度。

```java
   public String[] findWords(String[] words) {
        Map<Character, Integer> map = new HashMap<>(32);
       // 初始化数据
        generateData(map);

        List<String> result = new ArrayList<>();

        for (String word : words) {
            // 转成小写操作
            String rep = word.toLowerCase();

            int row = map.get(rep.charAt(0));
            int rowOrigin = row;

            boolean canAdded = true;

            if (word.length() == 1) {
                // 如果仅包含一个字符，则无需再次遍历
                result.add(word);
            }

            for (int i = 1; i < word.length(); i++) {

                row = map.get(rep.charAt(i));
                if (row == rowOrigin) {

                    if (i == word.length() - 1 && canAdded) {
                        result.add(word);
                    }
                } else {
                    canAdded = false;
                }
            }
        }

        return result.stream().toArray(String[]::new);
    }

    private void generateData(Map<Character, Integer> map) {
        map.put('q', 1);
        map.put('w', 1);
        map.put('e', 1);
        map.put('r', 1);
        map.put('t', 1);
        map.put('y', 1);
        map.put('u', 1);
        map.put('i', 1);
        map.put('o', 1);
        map.put('p', 1);

        map.put('a', 2);
        map.put('s', 2);
        map.put('d', 2);
        map.put('f', 2);
        map.put('g', 2);
        map.put('h', 2);
        map.put('j', 2);
        map.put('k', 2);
        map.put('l', 2);

        map.put('z', 3);
        map.put('x', 3);
        map.put('c', 3);
        map.put('v', 3);
        map.put('b', 3);
        map.put('n', 3);
        map.put('m', 3);
    }
```

### 优化

冷静下来仔细想想，上面的代码看着很长，主要初始化 HashMap 就占了很长，我们能不能不用 HashMap呢？因为题目中说到了可以认为输入仅包含字母表中字符，所以其实我们不用这么复杂，用 ASCII 码代替我们来存储映射关系。有点模糊？直接上代码。

```java
public static String[] findWords1(String[] words) {
        int[] alphabet = new int[]{2, 3, 3, 2, 1, 2, 2,
                2, 1, 2, 2, 2, 3, 3,
                1, 1, 1, 1, 2, 1,
                1, 3, 1, 3, 1, 3};

        List<String> result = new ArrayList<>();

        for (String word : words) {

            int line = 0;
            boolean flag = true;

            for (char c : word.toCharArray()) {
                int index = c > 96 ? c - 97 : c - 65;

                if (line == 0) {
                    line = alphabet[index];
                } else {
                    if (line != alphabet[index]) {
                        flag = false;
                        break;
                    }
                }
            }
            if (flag) {
                result.add(word);
            }
        }

        String[] res = new String[result.size()];
        return result.toArray(res);
    }
```

虽然主体机构类似，但代码看起来精简了不少。