# [93. 复原 IP 地址](https://leetcode.cn/problems/restore-ip-addresses/)

```javascript
/**
 * @param {string} s
 * @return {string[]}
 */
const restoreIpAddresses = (s) => {
    const res = [], path = [], len = s.length;
    getIp(0);
    return res;
    function getIp(index) {
        if (path.length > 4) return;
        if (path.length === 4 && index === len) {
            res.push(path.join('.'));
            return;
        }
        for (let i = index; i < len; i++) {
            const str = s.slice(index, i + 1);
            // 依据题意去除无效 IP 地址
            if (str.length > 3 || Number(str) > 255) break;
            if (str.length > 1 && str[0] === '0') break;
            path.push(str);
            getIp(i + 1);
            path.pop();
        }
    }
}
```