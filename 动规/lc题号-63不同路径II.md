# [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)
```typescript
function uniquePathsWithObstacles(obstacleGrid: number[][]): number {
    const m = obstacleGrid.length;
    const n = obstacleGrid[0].length;
    const dp: number[][] = Array.from(Array(m), () => new Array(n).fill(0));
    if (obstacleGrid[0][0] === 1 || obstacleGrid[m - 1][n - 1] === 1) return 0;

    // [i][0] 对应是列，则要对应 obstacleGrid.length -> m
    for (let i = 0; i < m; i++) {
        if (obstacleGrid[i][0] === 1) {
            dp[i][0] = 0;
            break; // 数组均初始化为 0 则可以直接break;
        } else {
            dp[i][0] = 1;
        }
    }

    // [0][i] 对应是行，则要对应 obstacleGrid.length -> n
    for (let i = 0; i < n; i++) {
        if (obstacleGrid[0][i] === 1) {
            dp[0][i] = 0;
            break; // 数组均初始化为 0 则可以直接break;
        } else {
            dp[0][i] = 1;
        }
    }
    
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 1) {
                dp[i][j] = 0;
            } else {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }

    return dp[m - 1][n - 1];
};
```