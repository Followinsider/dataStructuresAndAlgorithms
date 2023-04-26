# [40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)

~~~javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
const combinationSum2 = function(candidates, target) {
    const res = [], path = [], sum = 0, len = candidates.length;
    candidates.sort((a, b) => a - b);
    getCombinationSum(0, sum);
    function getCombinationSum(index, sum) {
        if (sum === target) {
            res.push([...path]);
            return;
        }
        for (let i = index; i < len; i++) {
            const val = candidates[i];
            if (i > index && candidates[i - 1] === val) continue; // 当 i > index 说明应该换为相邻节点且根据题意要求相邻不能重复
            if(val > target - sum) break;
            sum += val;
            path.push(val);
            getCombinationSum(i + 1, sum);
            sum -= val; // 这里就是上面continue出来后回溯
            path.pop();
        }
    };
    return res;
};
~~~

