# [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/)
```typescript
function change(amount: number, coins: number[]): number {
    // coins[1, 2, 5] amount 5 ->  4 种方式
    const dp:number[] = new Array(amount + 1).fill(0);
    dp[0] = 1;
    const len:number = coins.length;
    // 先遍历物品
    for (let i = 0; i < len; i++) {
        // 其次容量,完全背包是 <= ; 01背包是 >= 关键在于是否可重复拿
        for (let j =  coins[i]; j <= amount; j++) {
            dp[j] += dp[j - coins[i]];
        }
    }
    return dp[amount];
};
```