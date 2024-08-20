# 买卖股票的最佳时机

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i `天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。

## 示例 1:
>### 输入: 
>prices = [7,1,5,3,6,4]
>### 输出: 
>5
>### 解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。

## 示例 2:
>### 输入: 
>prices = [7,6,4,3,1]
>### 输出: 
>0
>### 解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

## 代码：
1.
```c#
public class Solution {
    const int FREE = 0, HOLD = 1;

    public int MaxProfit(int[] prices) {
        int n = prices.Length;
        int[][] dp = new int[n][];
        for (int i = 0; i < n; i++) {
            dp[i] = new int[2];
        }
        dp[0][FREE] = 0;
        dp[0][HOLD] = -prices[0];
        for (int i = 1; i < n; i++) {
            dp[i][FREE] = Math.Max(dp[i - 1][FREE], dp[i - 1][HOLD] + prices[i]);
            dp[i][HOLD] = Math.Max(dp[i - 1][HOLD], -prices[i]);
        }
        return dp[n - 1][FREE];
    }
}
```
2.
```c#
public class Solution {
    public int MaxProfit(int[] prices) {
        int maximumProfit = 0, prevMin = prices[0];
        int n = prices.Length;
        for (int i = 1; i < n; i++) {
            maximumProfit = Math.Max(maximumProfit, prices[i] - prevMin);
            prevMin = Math.Min(prevMin, prices[i]);
        }
        return maximumProfit;
    }
}
```
3.
```c#
public class Solution {
    public int MaxProfit(int[] prices) {
        int n = prices.Length;
        int dpFree = 0, dpHold = -prices[0];
        for (int i = 1; i < n; i++) {
            dpFree = Math.Max(dpFree, dpHold + prices[i]);
            dpHold = Math.Max(dpHold, -prices[i]);
        }
        return dpFree;
    }
}
```