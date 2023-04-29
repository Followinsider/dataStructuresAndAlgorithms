#  [131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)
~~~javascript
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function(s) {
    const res = [], path = [], len = s.length;
    const findPath = (index) => {
        if (index >= len) {
            res.push([...path]);
            return;
        }
        for (let i = index; i < len; i++) {
            if (!isPalindrome(s, index, i)) continue;
            path.push(s.slice(index, i + 1));
            findPath(i + 1);
            path.pop();
        }
    }
    findPath(0);
    return res;
};
function isPalindrome(s, l, r) {
    for (let i = l, j = r; i < j; i++, j--) {
        if (s[i] !== s[j]) return false;
    }
    return true;
}
~~~

