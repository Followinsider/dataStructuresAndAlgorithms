# [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)
```typescript
// 第三版本加多一个限制 至多卖两次求最大利润
/**
    dp[i][1] 表示第1次持有股票
    dp[i][2] 表示第1次不持有股票
    dp[i][3] 表示第2次持有股票
    dp[i][4] 表示第2次不持有股票
*/
function maxProfit(prices: number[]): number {
    
    const len = prices.length;
    if (len === 0 || len === 1) return 0;
    // 这里子数组长度为5代表五种状态，其中第一种不操作就没在代码体现了
    const dp: number[][] = new Array(len).fill(0).map(_ => new Array(5).fill(0));
    dp[0][1] = -prices[0];
    // 因为第2次持有 前 需要先卖出的，所以买入卖出利润和为0，此时就回到-prices[0]
    dp[0][3] = -prices[0];
    for (let i = 1; i < len; i++) {
        dp[i][1] = Math.max(dp[i - 1][1], 0-prices[i]);
        dp[i][2] = Math.max(dp[i - 1][2], dp[i - 1][1] + prices[i]);
        dp[i][3] = Math.max(dp[i - 1][3], dp[i - 1][2] - prices[i]);
        dp[i][4] = Math.max(dp[i - 1][4], dp[i - 1][3] + prices[i]);
    }
    return Math.max(dp[len - 1][2], dp[len - 1][4]);
};
```