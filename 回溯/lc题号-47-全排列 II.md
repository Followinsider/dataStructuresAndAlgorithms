# [47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
// 相比46题 给了一个可包含重复数字的序列
const permuteUnique = (nums) => {
    const res = [], path = [], len = nums.length;
    const hasUse = new Array(len).fill(0);

    nums.sort((a, b) => a - b); // 注意要先排序，后续判断是否使用是依据相邻元素 
    getPermuteUnique(hasUse);
    return res;
    
    function getPermuteUnique(hasUse) {
        if (path.length === len) {
            res.push([...path]);
            return;
        }
        for (let i = 0; i < len; i++) {
            if (i > 0 && nums[i] === nums[i - 1] && !hasUse[i - 1]) { // hasUse[i]的判断决定是树层上去重或者树枝上去重
                continue;
            }
            
            if (!hasUse[i]) { // i为 0 不会进入上面的判断, 确保不重复元素
                hasUse[i] = 1;
                path.push(nums[i]);
                
                getPermuteUnique(hasUse);

                hasUse[i] = 0;
                path.pop();
            }
        }
    }
}
```
> 树层上去重(used[i - 1] == false)，的树形结构如下：
![](https://code-thinking-1253855093.file.myqcloud.com/pics/20201124201406192.png)

>树枝上去重（used[i - 1] == true）的树型结构如下：
![](https://code-thinking-1253855093.file.myqcloud.com/pics/20201124201431571.png)
