# [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
```typescript
function maxProfit(prices: number[]): number {
    let result: number = 0;
    for (let i = 1; i < prices.length; i++) {
        // 跨一大步也能拆分成多个小步，小步趋近 5-1 -> 5-4+4-3+3-2+2-1
        result += Math.max((prices[i] - prices[i - 1]), 0);
    }
    return result;
};
```