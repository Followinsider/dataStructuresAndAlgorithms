#  [90. 子集 II](https://leetcode.cn/problems/subsets-ii/)
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function(nums) {
    const res = [], path = [], hasVal = [], len = nums.length;
    getSubsetWithDup(0);
    return res;
    function getSubsetWithDup(index) {
        const val = [...path].sort((a, b) => a - b).join('');
        if (!diffElement(hasVal, val)) {
            res.push([...path]);
            hasVal.push(val);
        }

        for (let i = index; i < len; i++) {
            path.push(nums[i]);
            getSubsetWithDup(i + 1);
            path.pop();
        }
    }
};
function diffElement(hasVal, newVal) {
    for (let i = 0; i < hasVal.length; i++) {
        if (hasVal[i] === newVal) return true;
    };
    return false;
}
```