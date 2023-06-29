# [188. 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)
```typescript
function maxProfit(k: number, prices: number[]): number {
    const len = prices.length;
    // 第四个版本中 k 指定是 那会直接子数组长度是5=> 5 = 2 * 2 + 1,子数组长度表示股票能被操作次数体现的股票持有或者不持有状态或者不操作（不操作可以不管，默认给0了）
    const child_len = 2 * k + 1;
    const dp: number[][] = new Array(len).fill(0).map(_ => new Array(2 * k + 1).fill(0));
    // console.log(dp);

    /**
        初始值 奇数为股票价格，偶数为0
     */
    for (let i = 1; i < child_len; i+= 2) {
        dp[0][i] = -prices[0];
    }
    // console.log(dp);
    /**
        dp[i][j + 1] 第 i 天 奇数次 持有股票的情况
        dp[i][j + 2] 第 i 天 偶数次 不持有股票的情况
        可以发现，本题其实就是把第三个版本股票买卖的 扩展成通用格式的
     */
    for (let i = 1; i < len; i++) {
        for (let j = 0; j < child_len; j += 2) {
            dp[i][j + 1] = Math.max(dp[i - 1][j + 1], dp[i - 1][j] - prices[i]);
            dp[i][j + 2] = Math.max(dp[i - 1][j + 2], dp[i - 1][j + 1] + prices[i]);
        }
    }
    // console.log(dp);
    // 最后 2 * k 不持有 利润是最大的
    return dp[len - 1][2 * k];
};
```