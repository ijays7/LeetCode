## Count Primes

Count the number of prime numbers less than a non-negative number, **n**.

**Example:**

```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

## Solution

这道题的意思是统计从0到非负数 n 之间有多少个素数。

这道题最容易想到暴力解法，遍历从2到 n ，判断这个数是不是素数，是则加一。这样做可行，但是比较麻烦。实际上这里需要了解一个数学技巧，这样就可以很快求出结果。

这里我们要了解到 [埃拉托斯特尼筛法](https://baike.baidu.com/item/%E5%9F%83%E6%8B%89%E6%89%98%E6%96%AF%E7%89%B9%E5%B0%BC%E7%AD%9B%E6%B3%95)，即

> 要得到自然数n以内的全部素数，必须把不大于 $$ \sqrt n$$ 的所有素数的倍数剔除，剩下的就是素数。
>
> 给出要筛[数值](https://baike.baidu.com/item/%E6%95%B0%E5%80%BC)的范围n，找出以内的[素数](https://baike.baidu.com/item/%E7%B4%A0%E6%95%B0)。先用2去筛，即把2留下，把2的倍数剔除掉；再用下一个[质数](https://baike.baidu.com/item/%E8%B4%A8%E6%95%B0)，也就是3筛，把3留下，把3的倍数剔除掉；接下去用下一个质数5筛，把5留下，把5的[倍数](https://baike.baidu.com/item/%E5%80%8D%E6%95%B0)剔除掉；不断重复下去......

有了上面的知识，我们就可以写出代码了。

```java
  public int countPrimes(int n) {

        int count = 0;
        double sqrted = Math.sqrt(n);
        boolean[] canComposite = new boolean[n];

        for (int i = 2; i < n; i++) {
            if (!canComposite[i]) {
                count++;
                if (i < sqrted) {
                    for (int j = i * i; j < n; j = j + i) {
                        canComposite[j] = true;
                    }
                }
            }
        }

        return count;
    }
```

