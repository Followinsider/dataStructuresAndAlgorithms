# [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
```typescript
// dp数组状态转移
/**
    dp[i][0]: 第i天持有股票的最大现金
    dp[i][1]: 第i天不持有股票的最大现金
*/
function maxProfit(prices: number[]): number {
    const length = prices.length;
    if (length === 0) return 0;
    // 用这个定义dp数组超出内存了
    // let dp: number[][] = new Array(prices.length).fill(0).map(_ => new Array(prices.length));
    // dp[0][0] = -prices[0];
    // dp[0][1] = 0;

    const dp: number[][] = [];
    dp[0] = [-prices[0], 0];

    for (let i = 1; i < prices.length; i++) {
        dp[i] = [];
        // 持有股票 -> 单次 买入（此时买入情况要加上前边可能有的收益）或者不作为同上一次持有
        dp[i][0] = Math.max(-prices[i] + dp[i - 1][1], dp[i - 1][0]);
        // 不持有股票 -> 单次 卖出或者不作为同上一次不持有
        dp[i][1] = Math.max(dp[i - 1][0] + prices[i], dp[i - 1][1]);
    }
    console.log(dp);
    return dp[prices.length - 1][1];

};
```