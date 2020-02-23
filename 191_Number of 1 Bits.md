## Number of 1 Bits

Write a function that takes an unsigned integer and return the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

**Example 1:**

```
Input: 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.
```

**Example 2:**

```
Input: 00000000000000000000000010000000
Output: 1
Explanation: The input binary string 00000000000000000000000010000000 has a total of one '1' bit.
```



## Solution

这道题是题目给的很简单，就是计算二进制数中1 的个数。

#### Approach1

我们知道，1 与上0 等于0，1与上1 等于1，所以可以通过进行与操作来判断该位上是不是1。

因此第一种方法的思路就是遍历输入的二进制数，将每一位和1 进行与操作，记下其中等于1 的个数，即为二进制数中1 的个数。

```java
public int hanmingWeight(int n) {
        int count = 0;
        int mask = 1;

        for (int i = 0; i < 32; i++) {
        // 为什么是32？因为 Java 中int 占4个字节
            if ((mask & n) != 0) {
                count++;
            }

         // 检查下一位时，左移1位 
            mask <<= 1;
        }
        return count;
    }
```



#### Approach2

这道题还有一种非常巧妙的方法，是官方解法的一种，同时也是[牛客网上类似题目的最佳答案](https://www.nowcoder.com/questionTerminal/8ee967e43c2c4ec193b040ea7fbb10b8)。

他们的思路是不在检查数字的每一位，而是不断把数字的最后一个 **1** 反转，并把计数器加1，当数字变成0 的时候返回最终的结果。

上面的话有一点抽象，简单来说就是如果1 个整数不为0，**那么它至少有一位上是1**。如果我们把这个数减1，那么原来处在整数最右边的1 就会变成0，原来在1 后面的所有0 都会变成1（如果1 后面还有0 的话 ）。如果这个时候，我们将原来的整数与减1 之后的做与运算，原来会把原来整数的最后一位1 变成**0**。

举个例子，二进制数1100 进行减1 操作之后，得到的结果是1011，将1100 与1011 进行与操作之后，得到1000，印证了上面的结果，将最后一位1 变成了0。所以我们就可以循环这个数，不断让它和它减1 的值进行与操作，知道最后的结果变成0，记下循环的次数即可。上代码。

```java
 public int hanmingWeight2(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n = n & (n - 1);
        }
        return count;
    }
```



上面的两种方式时间复杂度都是 O(1)，因为n 的值都是32。不过下面的代码更有技巧，需要知道 n & (n - 1) 有什么意义，代码上写来更简洁。

