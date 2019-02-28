## Best Time to Buy and Sell Stock II

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

## Solution

这道题是买卖股票系列题中的一道。

题目意思是给定一个数组，数组中每个元素代表了每天的股价，每天可以交易多次，求股票交易的最大利润。为了方便理解，我们先来看看 Example。在第2天以1元买入，在第3天卖出，净赚4元。接下来在第4天买入，第5天卖出，净赚3元，所以总的利润是3 + 4 = 7元。

因为题目没有太多的限制，且一天可以交易多次，所以我们可以使用***贪心算法***，我们可以通过每一天的最大利润推导出最大的利润，即子问题的最优解递推到问题的最优解。

什么意思呢？上面也说道了，题目中没有交易次数等限制，所以我们仅需关心当前如何利润最大，即总是做当前最好的选择即可。比如说，上面第一天股价7元，第二天股价1元，交易的话不会赚钱，所以跳过；第三天股价5元，所以我们可以在第2天买入，第三天卖出，净赚4元；而第四天股价低于第三天，因此不交易。以此类推，我们只要判断下一天的股价高于当前，即进行交易即可。

使用贪心算法的话总的时间复杂度为 O(n)，n 为数组的长度，空间复杂度为 O(1)。

```java
  public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int totalProfit = 0;

        for (int i = 0; i < prices.length; i++) {

            if (i < prices.length - 1 && prices[i] < prices[i + 1]) {
                totalProfit = totalProfit - prices[i] + prices[i + 1];
            }
        }
        return totalProfit;
    }
```

