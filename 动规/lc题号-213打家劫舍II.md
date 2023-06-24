# [213. 打家劫舍 II](https://leetcode.cn/problems/house-robber-ii/)
```typescript
function rob(nums: number[]): number {
    // dp[i] 代表 i 间房下所能偷的最高金额,此题比起第一版本在与成环，那么环拆分两条路就同第一版本了
    const len: number = nums.length;
    if (len === 0) return 0;
    if (len === 1) return nums[0];
    const oneRoad: number = robRange(nums, 0, len - 2);
    const anotherRoad: number = robRange(nums, 1, len - 1);
    return Math.max(oneRoad, anotherRoad);
    
};
const robRange = (nums: number[], left:number, right: number) => {
    // 这里重新切割 nums 成 newNums, 在于后续遍历获取 dp[i]时，nums[i]能正确获取
    const newNums = nums.slice(left, right + 1);
    const len = newNums.length;
    const dp: number[] = new Array(len).fill(0);

    dp[0] = newNums[0];
    dp[1] = Math.max(dp[0], newNums[1]);

    for (let i = 2; i < len; i++) {
        dp[i] = Math.max(dp[i - 2] + newNums[i], dp[i - 1]);
    }
    // console.log(dp);
    return dp[len - 1]
    
}
```