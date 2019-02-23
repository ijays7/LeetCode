## Climbing Stairs

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

## 分析

这道题目的意思是这样的，有一个 n 级的楼梯，你一次可以走1级或者2级，问有多少种不同的方法走到顶部。

这道题的思路首先当然可以是暴力破解，穷举所有的可能性，但肯定不是我们想要的方法。我们冷静下来仔细分析下。

### Approach1：递归

假设现在只有10级楼梯，走到终点的时候有几种方式呢？答案是两种，要么最后走一步，要么最后走两步，即最后要么在第8级楼梯上，要么最后在第9级楼梯上。再想一下，这两种方式之间有什么关系呢？

为了方便描述，我们将走到10楼记为 f(10)，那么走到9楼和8楼则被称为 f(9)，f(8)。题目中闻到有多少种不同的方式走到顶部，那么是不是应该是走到9楼的走法数量加上8楼的走法数量呢？（仔细考虑下），即：
$$
f(10) = f(9) + f(8)
$$
继续顺着这个思路，走到9楼的走法数量又等于走到8楼的走法数量，可以一直走下去，一直到哪呢？

当楼梯只有一级时，只有一种走法，当楼梯只有两级时，只有2中走法。

通过上面的思路，我们就可以得到一个结论了：
$$
f(n) = f(n-1) + f(n-2),(n>=3)
$$
那么，这套递归的代码我们也就有了。

```java
  public int climbStairs(int n) {
        // 递归
        if (n < 1) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        return climbStairs(n - 1) + climbStairs(n - 2);
  }
```

### Approach2：动态规划

当我们满心欢喜的用上面的代码提交的时候，看到的是 “Runtime：8417ms，faster than 5% of Java Online Submissions”。What the heck，man！

仔细看下我们的代码，为什么 Runtime 会那么长，因为涉及到了大量的重复计算，比如等式左边计算 f(8) 的时候，会去计算 f(7) 和 f(6)，而右边本来就会去计算 f(7)，这样算下来，整体的时间复杂度接近于 O($$2^n$$)，并且随着 n 的取值不断变大，函数的调用栈会越来越长，而分给程序的栈空间是有限的，所以这个递归并不是解决这个问题的最佳方法。

上面的思路都是从上而下的，我们来考虑下自下而上的方式。

上文已经明确，1楼只有1种走法，2楼只有2种走法，那么三楼呢？答案是3种走法，如何来的呢？是 f(1) 和 f(2) 相加而来。继续往下走，4楼就有5种走法，也是通过 f(3) 与 f(2) 相加得来。我们还可以往下推，但是已经可以可以得到一个结论：走 n 级楼梯的方法数，只与它的前两级楼梯走法数有关系，这也印证了上文的递推公式。上代码。

```java
 public int climbStairs(int n) {
       
         // DP
        if (n < 1) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }

        int a = 1;
        int b = 2;
        int temp = 0;
        for (int i = 2; i < n; i++) {
            temp = a + b;
            a = b;
            b = temp;
        }
        return temp;

    }
```

上面的代码中 a ，b 分别设置了成了走第一楼和第二楼的走法数，当楼层数继续增加时，在每一循环中，用 temp 保存当前走的总方法数，而 a，b 则保存了之前的两个状态。

上面的代码时间复杂度为 O(n)，空间复杂度为 O(1)。当提交完代码，发现 “Runtime：1ms，faster than 100% of Java submissions”，Perfect！

