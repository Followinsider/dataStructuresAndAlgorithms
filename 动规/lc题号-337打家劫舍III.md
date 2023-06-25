# [337. 打家劫舍 III](https://leetcode.cn/problems/house-robber-iii/)
```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
// 状态标记化后序遍历-dp状态转移
// type SelectedValue = [number, number];

// function dfs (node: TreeNode | null): SelectedValue {
//     if (node === null) return [0, 0];
//     let left: SelectedValue = dfs(node.left);
//     let right: SelectedValue = dfs(node.right);

//     // 不偷当前节点
//     const noSelected: number = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
//     // 偷当前节点
//     const selected: number = left[0] + right[0] + node.val;
//     return [noSelected, selected];
// }
// function rob(root: TreeNode | null): number {
//     const result: SelectedValue = dfs(root);
//     console.log(result);
//     return Math.max(...result);
// };

// 记忆化后序遍历
const memory: Map<TreeNode, number> = new Map();
function rob(root: TreeNode | null): number {
    if (root === null) return 0;
    if (memory.has(root)) return memory.get(root);

    // 不偷当前节点
    const res1: number = rob(root.left) + rob(root.right);

    // 偷当前节点
    let res2: number = root.val;

    if (root.left) {
        res2 += rob(root.left.left) + rob(root.left.right);
    }

    if (root.right) {
        res2 += rob(root.right.left) + rob(root.right.right);
    }
    
    const res:number = Math.max(res1, res2);
    memory.set(root, res);
    return res;
};

```