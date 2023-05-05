# [51. N 皇后](https://leetcode.cn/problems/n-queens/)
```javascript
/**
 * @param {number} n
 * @return {string[][]}
 */
const solveNQueens = (n) => {
    const chess = new Array(n).fill([]).map(() => new Array(n).fill('.'));
    const res = [];

    const isValid = (row, col, chess, n) => {
        for (let i = 0; i < row; i++) {
            if (chess[i][col] === 'Q') return false;
        }
        for (let i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (chess[i][j] === 'Q') return false;
        }
        for (let i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
            if (chess[i][j] === 'Q') return false;
        }
        return true;
    }
    const transformValue = (doubleArray) => {
        let tempVal = [];
        doubleArray.forEach(row => {
            let str = '';
            row.forEach(val => {
                str += val;
            });
            tempVal.push(str);
        })
        return tempVal;
    }
    const getQueen = (row, chess) => {
        if (row === n) {
            res.push(transformValue(chess));
            return;
        }
        for (let col = 0; col < n; col++) {
            if (isValid(row, col, chess, n)) {
                chess[row][col] = 'Q';
                getQueen(row + 1, chess);
                chess[row][col] = '.';
            }
        }
    };
    getQueen(0, chess);
    return res;
}
```