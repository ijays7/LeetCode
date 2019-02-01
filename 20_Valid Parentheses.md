## Valid Parentheses

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

## Solution

这道题的考点是使用栈这种数据结构。

这道题目意思是判断括号是否合法。如何判断括号是否合法呢？必须要同等级的括号互相匹配才行，比如 “(” 和 “)”。我们解决这道题的思路是将字符串转换为字符数组，然后将每个元素分别入栈，但是在入栈之前判断当前栈顶的元素和即将入栈的元素能否匹配，如果能够匹配，那么栈顶的元素直接出栈，直到最后一个元素为止。最后我们判断当前栈中是否还有元素。下面的代码代码中我们用一个 map 来保存括号匹配的对应关系。

时间复杂度：对于栈这种数据结构，每一个元素入栈和出栈时间复杂度是 O(1) 的，然后对于字符串的 n 个元素都循环一次，所以总的时间复杂度为 O( n )。

空间复杂度：最坏的情况每个元素都入栈一次，所以空间复杂度为 O( n )。

```java
 public static boolean isValid(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        Stack<Character> stack = new Stack<>();
        Map<Character, Character> pairs = new HashMap<>(4);
        pairs.put('(', ')');
        pairs.put('[', ']');
        pairs.put('{', '}');

        for (Character c : s.toCharArray()) {
            if (pairs.containsKey(c)) {
                stack.push(c);
            } else {
                Character character = pairs.get(c);
                if (!stack.isEmpty() && c.equals(pairs.get(stack.peek()))) {
                    stack.pop();
                } else{
                    return false;
                }
            }
        }


        return stack.isEmpty();
    }
```

Kotlin版：

```kotlin
fun isValid(s: String): Boolean {

    val stack = mutableListOf<Char>()
    val pairs = mapOf<Char, Char>('(' to ')', '[' to ']', '{' to '}')

    s.toCharArray().forEach {
        if (pairs.containsKey(it)) {
            stack.add(it)
        } else {
            if (!stack.isEmpty() && it == pairs[stack.last()]) {
                stack.removeAt(stack.size - 1)
            } else {
                return false
            }
        }
    }

    return stack.isEmpty()
}
```



LeetCode Discussion 中的 Java 做法：

这个做法大同小异，没有使用 map 存储映射关系，因为这道题匹配的内容很少，直接枚举各种匹配的情况，殊途同归。

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<Character>();
    for(int i=0, L=s.length(); i<L; i++) {
        char ch = s.charAt(i);
        if(ch==')' || ch==']' || ch=='}') {
            if(stack.isEmpty()) return false;
            if(ch==')' && stack.pop()!='(') return false;
            if(ch==']' && stack.pop()!='[') return false;
            if(ch=='}' && stack.pop()!='{') return false;
        }
        else stack.push(ch);
    }
    return stack.isEmpty() ? true : false;
}
```

