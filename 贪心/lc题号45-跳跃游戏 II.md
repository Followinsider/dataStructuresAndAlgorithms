# [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)
```typescript
function jump(nums: number[]): number {
    const length: number = nums.length;
    let curIndex: number = 0,
        nextIndex: number = 0;
    let index: number = 0;
    let stepNum: number = 0;
    while (index < length - 1) {
        nextIndex = Math.max(nextIndex, index + nums[index]);
        if (index === curIndex) {
            curIndex = nextIndex;
            stepNum++;
        }
        index++;
    }
    return stepNum;
};
```