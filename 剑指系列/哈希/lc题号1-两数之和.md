# [1. 两数之和](https://leetcode.cn/problems/two-sum/)
```typescript
function twoSum(nums: number[], target: number): number[] {
    let map:Map<number, number> = new Map();
    for (let i = 0; i < nums.length; i++) {
        let tempVal = target - nums[i];
        if (map.has(tempVal)) {
            return [map.get(tempVal), i];
        }
        map.set(nums[i], i);
    }
};
```