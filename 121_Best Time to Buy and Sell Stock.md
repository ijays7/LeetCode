## Best Time to Buy and Sell Stock

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

## Solution

这道题是买卖股票系列的第一题。[第二题在这里](https://github.com/ijays7/LeetCode/blob/master/122_Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.md)

题目中给定一个整形数组，数组中的每个元素代表每天的股价。这里规定只能完成1笔交易，即买入1次和卖出1次，并且必须先买入才能卖出，我们需要设计出一个算法求出最大的利润。

我们可以记录两个状态，一个是当前的最大利润，一个是当前数组中的最小值，知道之前数组中的最小值我们就可以计算出当前利润的最大值，整体算法还是比较巧妙。

此算法时间复杂度为 O(n)，空间复杂度为 O(1)。

```java
 public int maxProfit(int[] prices) {

        if (prices == null || prices.length == 0) {
            return 0;
        }

        int maxProfit = 0;
        int minNum = Integer.MAX_VALUE;

        for (int i = 0; i < prices.length; i++) {
            if (minNum != Integer.MAX_VALUE && prices[i] - minNum > maxProfit) {
                maxProfit = prices[i] - minNum;
            }


            if (prices[i] < minNum) {
                minNum = prices[i];
            }
        }
        return maxProfit;
    }
```

