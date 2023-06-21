# 双指针法
## 移除元素
```javascript
function removeElement(nums, target) {
  let fast = slow = 0;
  for(; fast < nums.length; fast++) { // fast每次递增次数大于等于1
    if (nums[fast] !== target) {
      nums[slow++] = nums[fast];
    };
    fast++;
  };
  return slow;
}
```

## 反转字符串
```javascript
function reverseStr(s) {
	if (s.length <= 1) return s;
  let res = s.split('');
  let left = 0, right = res.length - 1;
  while(left < right) {
    [res[right], res[left]] = [res[left], res[right]];
    left++;
    right--;
  }
  return res.join('');
}
```
## 替换空格
```javascript
// 空格替换成 -> %20
function replaceEmptySpace(s) {
	let res = s.split('');
  let sumEmptySpace = 0;
	for (let i = 0; i < res.length; i++) {
    if (res[i] === ' ') {
      sumEmptySpace++;
    };
  }
  let left = res.length - 1;
  let right = res.length + sumEmptySpace * 2 - 1;
  while (left >= 0) {
    if (nums[left] === ' ') {
      nums[right--] = '0';
      nums[right--] = '2';
      nums[right--] = '%';
    }else {
      nums[right--] = nums[left--];
    }
  }
  return res.join('');
}
```
## 翻转字符串里的单词
```javascript
// 全部翻转再单个按空格翻转,同时还要去除一些空格
function reverseWord(s) {
	
}

function reverseStr(s) {
	if (s.length <= 1) return s;
  let res = s.split('');
  let left = 0, right = res.length - 1;
  while(left < right) {
    [res[right], res[left]] = [res[left], res[right]];
    left++;
    right--;
  }
  return res.join('');
}

function removeEmptySpace(s) {
  let res = s.split('');
  const len = res.length;
  
  let fast = slow = 0;
  for (let i = 0; i < len; i++) {
    if (res[i] === ' ' && (i === 0 || res[i - 1] === ' ')) {
      fast++;
      continue;
    }
    
  }
}
```



## 翻转链表
```javascript
function reverseListNode(head) {
	if (!head || !head.next) {
    return;
  }
  let cur, temp, pre;
  cur = head, pre = null;
  while(cur) {
    temp = cur.next;
    cur.next = pre;
    pre = cur;
    cur = temp;
  }
  return p;
}
```
## 删除链表的倒数第 n 个节点
```javascript
// 快慢指针+虚拟头结点
function remove_N_ListNode(head, n) {
  let dummpyHead = new ListNode(null, head); // 虚拟头结点
  let fast = slow = dummpyHead;
  while(n--) {
    fast = fast.next;
  }
  // fast到达第n个节点
  while(fast && fast.next) {
    fast = fast.next;
    slow = slow.next;
  }
  slow.next = slow.next.next;
  return dummpyHead.next;
}
```
## 链表相交
```javascript
// 判断是否有环节点
function judgeCircleNode(headA, headB) {
  let p1 = headA;
  let p2 = headB;
  while(p1 !== p2) {
    if (!p1) {
      p1 = headB;
    }else {
      p1 = p1.next;
    }
    if (!p2) {
      p2 = headA;
    }else {
      p2 = p2.next;
    }
  }
  return p1;
}
```
## 环形链表(同时找到环入口)
```javascript
// 快慢指针 ->找到相遇节点
function findCircleStart(head) {
  let fast = head, slow = head.next;
  while(fast !== slow) {
    fast = fast.next.next;
    slow = slow.next;
  }
  // fast和slow相等，有可能是null，注意区分
  if (!fast) return null;
  // 找到相遇节点了，重新指定一个指针到开头head
  slow = head;
  while(fast !== slow) {
    fast = fast.next;
    slow = slow.next;
  }
  return slow;
}
```
## 三数之和
```javascript
// 三数之和为 0 , 双指针思想（注意得先排序），外层for循环 &&left && right
function threeSum(nums) {
  const res = [], len = nums.length // res存放三元组[[a,b,c]]
  // 将数组排序
  nums.sort((a, b) => a - b) // [-4,-1,-1,0,1,2]
  for (let i = 0; i < len; i++) {
      let l = i + 1, r = len - 1, iNum = nums[i] // l->1 r->5 iNum->-4
      // 数组排过序，如果第一个数大于0直接返回res
      if (iNum > 0) return res
      // 去重 -> 针对a
      if (i > 0 && iNum == nums[i - 1]) continue;
  
      while(l < r) {
          let lNum = nums[l], rNum = nums[r], threeSum = iNum + lNum + rNum
          // 三数之和小于0，则左指针向右移动
          if (threeSum < 0) l++;
          else if (threeSum > 0) r--;
          else {
              res.push([iNum, lNum, rNum])
              // 去重 针对b 和 c
              while(l < r && nums[l] == nums[l + 1]){
                  l++;
              }
              while(l < r && nums[r] == nums[r - 1]) {
                  r--;
              }
              l++;
              r--;
          }
      }
  }
  return res;
}
```
## 四数之和
```javascript
function fourSum(nums, target) {
  if (nums.length < 4) return [];
  nums.sort((a, b) => a - b);
  const res = [];
  const len = nums.length;
  for (let i = 0; i < len - 3; i++) {
    // 去重i
    // if (i === 0 && arr[i] > 0) return []; 四数之和的target不为0，则此处不能直接return;
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    for (let j = i + 1; j < len - 2; j++) {
      // 去重j
      if (j > i + 1 && nums[j] === nums[j - 1]) continue;
      let left = j + 1, right = len - 1;
      while(left < right) {
        let sum = nums[i] + nums[j] + nums[left] + nums[right];
        if (sum > target) {
          right--;
        }else if (sum < target) {
          left++;
        }else {
          res.push([ nums[i], nums[j], nums[left], nums[right] ]);
          while(left < right && nums[left] === nums[++left]) {
            continue;
          };
          while(left < right && nums[right] === nums[--right]) {
            continue;
          };
        }
      }
    }
  }
  return res;
}
```


# 栈结构
## 栈的特性与使用
简单栈的特点可以用一句话来概括，**先进后出**（LIFO）顺序。比如 Java 代码（解析在注释里）：
```java
Stack<Character> t = new Stack<Character>(); 
t.push('a'); 
t.push('b'); 
t.peek(); // 这里得到栈顶元素'b' 
t.pop();  // 这里将栈顶元素'b'弹出
t.peek(); // 此时栈顶元素为'a' 
t.pop();  // 这里将栈顶元素'a'弹出 
```
这部分代码片段执行效果如下图所示：
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679845881409-f9cea925-74a2-443f-a502-2d66dcd09544.gif#averageHue=%23fdfdfd&clientId=uedda4a7c-35ea-4&id=TQC4h&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uda7d17e7-ebd9-45c4-bd70-746385831bb&title=)
### 1.判断字符串括号是否合法
【**题目**】字符串中只有字符'('和')'。合法字符串需要括号可以配对。比如：
输入："()"
输出：true
**解释**：()，()()，(())是合法的。)(，()(，(()是非法的。
请你实现一个函数，来判断给定的字符串是否合法。
```java
boolean isValid(String s)
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26762664/1679845978183-50d9aaee-81ad-47af-9ce1-f6a9fc1d87a6.png#averageHue=%23f9f6f6&clientId=uedda4a7c-35ea-4&id=mMLUl&originHeight=295&originWidth=877&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27023&status=done&style=none&taskId=ud724f196-18ee-4383-8ccf-c4f05aceba1&title=)
```javascript
// 存放内容
// const isValid = str => {
//     const stack = [];
//     const arr = str.split("");
//     const len = arr.length;
//     if (len < 0) return;
//     for (let i = 0; i < len; i++) {
//         if (arr[i] === "(") {
//             stack.push(")");
//         }else {
//             if (stack.pop() !== arr[i]) {
//                 return false;
//             }
//         }
//     }
//     return stack.length === 0;
// }

// 由于存放的是单一 )，则可以计数器优化
// const isValid = str => {
//     let res = 0;
//     const arr = str.split("");
//     const len = arr.length;
//     if (len < 0) return;
//     for (let i = 0; i < len; i++) {
//         if (arr[i] === "(") {
//             res++;
//         }else if (arr[i] === ")"){
//             res--;
//         }
//     }
//     return res === 0;
// }


// 栈存放具体多个内容类型
// () [] {}
const isValid = str => {
  let stack = [];
  const arr = str.split("");
  const len = arr.length;
  if (len < 0) return;
  for (let i = 0; i < len; i++) {
    switch(arr[i]) {
      case "(":
        stack.push(")");
        break;
      case "[":
        stack.push("]");
        break;
      case "{":
        stack.push("}");
        break;
      default:
        if (stack.pop() !== arr[i]) return false;
        break;
    }
  }
  return stack.length === 0;
}
console.log(JSON.stringify(isValid("(([{}{{}}}]))")));
```
### 2.大鱼吃小鱼
【**题目**】在水中有许多鱼，可以认为这些鱼停放在 x 轴上。再给定两个数组 Size，Dir，Size[i] 表示第 i 条鱼的大小，Dir[i] 表示鱼的方向 （0 表示向左游，1 表示向右游）。这两个数组分别表示鱼的大小和游动的方向，并且两个数组的长度相等。鱼的行为符合以下几个条件:

1.  所有的鱼都同时开始游动，每次按照鱼的方向，都游动一个单位距离； 
2.  当方向相对时，大鱼会吃掉小鱼； 
3.  鱼的大小都不一样。 

输入：Size = [4, 2, 5, 3, 1], Dir = [1, 1, 0, 0, 0]
输出：3
请完成以下接口来计算还剩下几条鱼？
```java
int solution(int[] Size, int[] Dir);
```
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679845993696-915e4f3b-f3e4-4e5d-9b7b-bb158041fcd2.gif#averageHue=%23fafafa&clientId=uedda4a7c-35ea-4&id=YIHYt&originHeight=480&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ubb0eb9f0-057f-4889-aac6-25ac6f601d0&title=)
【**分析**】对于这道题而言，大鱼吃掉小鱼的时候，可以认为是一种**消除**行为。只不过与括号匹配时的行为不一样：

-  括号匹配是会**同时**把左括号与右括号消除掉； 
-  大鱼吃小鱼，**只会把小鱼**消除掉。 
```javascript
// SizeArr [4, 3, 2, 1, 5]; 值表示大小
// DireArr [0, 1, 0, 0, 0];  值表示方向 规定0为左，1为右
// res-> 2 表示最后只剩下两条鱼，大小分别为 4 和 5
// let sizeArr = [4, 3, 2, 1, 5];
// let direArr = [0, 1, 0, 0, 0];
let sizeArr = [10, 2, 2, 4, 3];
let direArr = [1, 1, 0, 1, 0];
function bigFishEatsmallFish(sizeArr, direArr) {
    let stack = []; // 存储索引
    const len = sizeArr.length;
    for(let i = 0; i < len; i++) {
        let hasEat = false;
        while(!isEmpty(stack) && direArr[i] === 0 && direArr[peek(stack)] === 1) { // direArr[i]即将要进栈，
            if (sizeArr[i] < sizeArr[peek(stack)]) {
                hasEat = true;
                break;
            }
            if (!hasEat) {
                stack.pop();
            }
        }
        if (!hasEat) {
            stack.push(i);
        }
    }
    console.log(stack);
    return stack.length;

}
function isEmpty(stack) {
    return stack.length === 0;
}
function peek(stack) {
    return stack[stack.length - 1];
}
console.log(bigFishEatsmallFish(sizeArr, direArr));
```
## 单调栈解题技巧
首先我们看一下**单调栈的定义**：单调栈就是指栈中的元素**必须**是按照**升序**排列的栈，或者是**降序**排列的栈。对于这两种排序方式的栈，还给它们各自取了小名。
升序排列的栈称为**递增栈**，如下图所示：
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679846149097-2edd59d6-872b-421e-9502-00cba096ac65.gif#averageHue=%23fefefe&clientId=uedda4a7c-35ea-4&id=GjeTI&originHeight=480&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uce9c9068-4f46-4f8f-8319-1f2984a1cc1&title=)

降序排列的栈称为**递减栈**，如下图所示：
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679846149083-8499c1df-d7ea-4726-8f68-aede6c981478.gif#averageHue=%23fefefe&clientId=uedda4a7c-35ea-4&id=dSuLq&originHeight=480&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u1a0ac711-21f2-4554-8b03-a5d5a46ef9e&title=)

_注意：示意图所展示的这两种栈是横向排列的。栈中元素的值，分别用不同高度的矩形来表示，值越大，矩形越高。_
接下来我们介绍一下递增栈的有序性，一句话：“**任何时候都需要保证栈的有序性**”。
递增栈的特性可以演示如下（上方数组是要依次入栈的元素）：
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679846149044-8d1637f5-78c0-4e79-8544-e71d3c33cf18.gif#averageHue=%23fefefe&clientId=uedda4a7c-35ea-4&id=dqV2Y&originHeight=480&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u7bc9a45d-6315-4f01-af10-1dbb9187665&title=)

递减栈的特性可以演示如下：
![](https://cdn.nlark.com/yuque/0/2023/gif/26762664/1679846149554-bcb63c79-40e4-428e-8957-eca48954e8c6.gif#averageHue=%23fefefe&clientId=uedda4a7c-35ea-4&id=uOX31&originHeight=480&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ud1d14ab9-948a-4fab-8b10-9fb711ee73f&title=)

通过这两个动图，我们可以总结出单调栈的特点，如下图所示：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26762664/1679846149176-9f5196a9-9035-42d3-a633-4afa27fcf8b9.png#averageHue=%23f9f5f4&clientId=uedda4a7c-35ea-4&id=AcwLY&originHeight=489&originWidth=982&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44367&status=done&style=none&taskId=ub5e26278-897c-4d24-b831-2e6dea50a68&title=)
### 3.找出数组中右边/左边比我大/小的元素
以找出数组中右边比我小的元素为例进行题意介绍：
【**题目**】一个整数数组 A，找到每个元素：右边第一个比我小的下标位置，没有则用 -1 表示。
输入：[5, 2]
输出：[1, -1]
**解释**：因为元素 5 的右边离我最近且比我小的位置应该是 A[1]，最后一个元素 2 右边没有比 2 小的元素，所以应该输出 -1。
```javascript
// 递增栈，小数消灭大数
// 递减栈，大数消灭小数
let arr = [4, 3, 2, 1, 5]; // return [1, 2, 3, -1, -1]
const result1 = findFirstSmallByRight(arr);
const result2 = findFirstBigByRight(arr);
const result3 = findFirstSmallByLeft(arr);
const result4 = findFirstBigByLeft(arr);
console.log(JSON.stringify(result1));
console.log(JSON.stringify(result2));
console.log(JSON.stringify(result3));
console.log(JSON.stringify(result4));


/**
 * 数组中右边第一个比我小的元素
 */

function findFirstSmallByRight(arr) {
  const len = arr.length; // 5
  let stack = [];
  let res = [];
  for (let i = 0; i < len; i++) { // 0 < 5
    while (!isEmpty(stack) && arr[i] < arr[peek(stack)]) {
      res[stack.pop()] = i;
    }
    stack.push(i); // [0, ] -> [1, ] -> [2, ] -> [3, ] -> [3, 4]
  }
  while(!isEmpty(stack)) {
    res[stack.pop()] = -1;
  }
  return res; // [1, 2, 3, -1, -1]
}

/**
 * 数组中右边第一个比我大元素
 */

function findFirstBigByRight(arr) {
  const len = arr.length; // 5
  let stack = [];
  let res = [];
  for (let i = 0; i < len; i++) { // 0 < 5
    while (!isEmpty(stack) && arr[i] > arr[peek(stack)]) {
      res[stack.pop()] = i;
    }
    stack.push(i); // [0, ] -> [0, 1, ] -> [0, 1, 2, ] -> [0, 1, 2, 3, ] -> [4, ]
  }
  while(!isEmpty(stack)) {
    res[stack.pop()] = -1;
  }
  return res; // [4, 4 ,4, 4, -1]
}

/**
 * 数组中元素左边离我最近且比我小的元素的位置
 */
function findFirstSmallByLeft(arr) { // [4, 3, 2, 1, 5]
  const len = arr.length; // 5
  let stack = [];
  let res = [];
  for (let i = len - 1; i >= 0 ; i--) { // 0 < 5
    while (!isEmpty(stack) && arr[i] < arr[peek(stack)]) {
      res[stack.pop()] = i;
    }
    stack.push(i); // [4, ] -> [3, ] -> [3, 2, ] -> [3, 2, 1, ] -> [3, 2, 1, 0]
  }
  while(!isEmpty(stack)) {
    res[stack.pop()] = -1;
  }
  return res; // [-1, -1, -1, -1, 3]
}

/**
 * 数组中元素左边离我最近且比我大的元素的位置
 */
function findFirstBigByLeft(arr) { // [4, 3, 2, 1, 5]
  const len = arr.length; // 5
  let stack = [];
  let res = [];
  for (let i = len - 1; i >= 0; i--) { // 0 < 5
    while (!isEmpty(stack) && arr[i] > arr[peek(stack)]) {
      res[stack.pop()] = i;
    }
    stack.push(i); // [4, ] -> [4, 3, ] -> [4, 2, ] -> [4, 1, ] -> [4, 0]
  }
  while(!isEmpty(stack)) {
    res[stack.pop()] = -1;
  }
  return res; // [-1, 0, 1, 2, -1]
}

function isEmpty(stack) {
  return stack.length === 0;
}
function peek(stack) {
  return stack[stack.length - 1];
}
```
### 4.字典序最小的 k 个数的子序列
【**题目**】给定一个正整数数组和 k，要求依次取出 k 个数，输出其中数组的一个子序列，需要满足：
1. **长度为 k**；
2.**字典序最小**。
输入：nums = [3,5,2,6], k = 2
输出：[2,6]
**解释**：在所有可能的解：{[3,5], [3,2], [3,6], [5,2], [5,6], [2,6]} 中，[2,6] 字典序最小。
所谓字典序就是，给定两个数组：x = [x1,x2,x3,x4]，y = [y1,y2,y3,y4]，如果 0 ≤ p < i，xp == yp 且 xi < yi，那么我们认为 x 的字典序小于 y。
```javascript
let nums = [3, 5, 2, 6, 100, 0, 1];
let k = 2;
console.log(miniDictionarySortOfK(nums, 2));
function miniDictionarySortOfK(nums, k) {
    const len = nums.length;
    if (len < k) return [];
    let stack = [];
    for (let i = 0; i < nums.length; i++) { 
        let num = nums[i];
        let left = len - i; // 4 -> 3 -> 2 -> 1
        while(!isEmpty(stack) && num < peek(stack) && (stack.length + left) > k) {
            stack.pop();
        };
        stack.push(num); // [3, ] -> [3, 5, ] -> [2, ]
    }
    return stack;
}
function isEmpty(stack) {
    return stack.length === 0;
}
function peek(stack) {
    return stack[stack.length - 1];
}
```

# 队列

# 二叉树
## 二叉树的遍历（前中后&层次）
### 递归法
```javascript
var preorderTraversal = function(root) {
    const result = [];
    const dfs = root => {
        if (!root) return;
        result.push(root.val);
        dfs(root.left);
        dfs(root.right);
    }
    dfs(root);
    return result;
};
```

```javascript
var inorderTraversal = function(root) {
    const result = [];
    const dfs = root => {
        if (!root) return;
        dfs(root.left);
        result.push(root.val);
        dfs(root.right);
    };
    dfs(root);
    return result;
};
```

```javascript
var postorderTraversal = function(root) {
    const result = [];
    const dfs = root => {
        if (!root) return;
        dfs(root.left);
        dfs(root.right);
        result.push(root.val);
    };
    dfs(root);
    return result;
};
```

```javascript
// 层次看迭代，学会一个模板我要打10个！
```

### 迭代法
```javascript
var preorderTraversal = function(root) {
    const result = [];
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if (!node) {
            result.push(stack.pop().val);
            continue;
        }
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
        stack.push(node); // 中
        stack.push(null); // 标志栈中第二个节点可以push进结果数组了
  
    };
    return result;
};
```

```javascript
var inorderTraversal = function(root) {
    const result = [];
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if (!node) {
            result.push(stack.pop().val);
            continue; 
        }
        if (node.right) stack.push(node.right); // 右
        stack.push(node); // 中
        stack.push(null);
        if (node.left) stack.push(node.left); // 左
    };
    return result;
};
```

```javascript
var postorderTraversal = function(root) {
    const result = [];
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if (!node) {
            result.push(stack.pop().val);
            continue;
        }
        stack.push(node); // 中
        stack.push(null);
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
    };
    return result; 
};
```

```javascript
var levelOrder = function(root) {
    const result = [];
    const queue = [];
    if (root) queue.push(root);
    while(queue.length) {
        const cur = [];
        const len = queue.length;
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            cur.push(node.val);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        result.push(cur);
    };
    return result;
};
```

## 二叉树的判断（是否相同、是否对称、是否子树、是否平衡）
### 是否相同
```javascript
var isSameTree = function(p, q) {
    if(p == null && q == null) 
        return true;
    if(p == null || q == null) 
        return false;
    if(p.val != q.val) 
        return false;
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
};
```

```javascript
// 迭代法
var isSameTree = function(p, q) {
    if (p === null && q === null) return true;

    const queue = [];
    queue.push(p);
    queue.push(q);

    while(queue.length) {
        const left = queue.shift();
        const right = queue.shift();
        if (left === null && right === null) continue;
        if (left === null || right === null || left.val !== right.val) return false;

        queue.push(left.left);
        queue.push(right.left);
        queue.push(left.right);
        queue.push(right.right);

    };
    return true;
}
```

### 是否对称
```javascript
var isSymmetric = function(root) {
    if (!root) return true;
    return mirrorTree(root.left, root.right);
};
function mirrorTree(left, right) {
    if (left === null && right !== null || left !== null && right === null) return false;
    if (left === null && right === null) return true;
    if (left.val !== right.val) return false;
    // 到这里就相等了，此时要判断子节点
    let outside = mirrorTree(left.left, right.right);
    let inside = mirrorTree(left.right, right.left);
    return outside && inside;
}
```

```javascript
// 迭代法--队列实现
var isSymmetric = function (root) {
    if (!root) return true;
    const queue = [];
    queue.push(root.left);
    queue.push(root.right);
    while(queue.length) {
        const left = queue.shift();
        const right = queue.shift();
        if (left === null && right === null) {
            continue;
        };
        if (left === null || right === null || left.val !== right.val) return false;
        queue.push(left.left);
        queue.push(right.right);
        queue.push(left.right);
        queue.push(right.left);
    };
    return true;
}

// 迭代法--栈实现（就是push进数组的顺序变化了）
var isSymmetric = function (root) {
    if (!root) return true;
    const stack = [];
    stack.push(root.left);
    stack.push(root.right);
    while(stack.length) {
        const left = stack.pop();
        const right = stack.pop();
        if (left === null && right === null) {
            continue;
        };
        if (left === null || right === null || left.val !== right.val) return false;
        stack.push(left.right);
        stack.push(right.left);
        stack.push(right.right);
        stack.push(left.left);
    };
    return true;
}
```

### 是否子树

### 是否平衡
```javascript
var isBalanced = function(root) {
    const getDepth = root => {
        if (!root) return 0;
        let leftDepth = getDepth(root.left);
        if (leftDepth === -1) return -1;
        let rightDepth = getDepth(root.right);
        if (rightDepth === -1) return -1;
        if (Math.abs(leftDepth - rightDepth) > 1) {
            return -1;
        }else {
            return 1 + Math.max(leftDepth, rightDepth);
        }
    }
    return !(getDepth(root) === -1);
};
```


## 二叉树的操作（翻转、求最大最小深度、求节点个数、求所有路径、求左叶子之和、找树左下角值、根据遍历顺序构造）

### 翻转
```javascript
var invertTree = function(root) {
    const queue = [];
    if (root) queue.push(root);
    while(queue.length) {
        const len = queue.length;
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            reverseTree(node, node.left, node.right);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
    };
    return root;
};
function reverseTree(node, left, right) {
    let temp = left;
    left = right;
    right = temp;
    node.left = left;
    node.right = right;
}
```
### 最大深度
```javascript
var maxDepth = function(root) {
    const result = [];
    const queue = [];
    if (root) queue.push(root);
    while(queue.length) {
        const len = queue.length;
        const cur = [];
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            cur.push(node.val);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        };
        result.push(cur);
    };
    return result.length;
};
```

### 最小深度
```javascript
var minDepth = function(root) {
    if (!root) return 0;
    const queue = [];
    queue.push(root);
    let depth = 1;
    while(queue.length) {
        const len = queue.length;
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            if (!node.left && !node.right) { //不存在子节点则可以返回深度了--keyCode
                return depth;
            }
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        };
        // 当前层次的节点 都有子节点，高度++--keyCode
        depth++;
    };
    return depth;
};
```

### 求节点数量
```javascript
var countNodes = root => {
    if (!root) return 0;
    const queue = [];
    queue.push(root);
    let result = 0;
    while(queue.length) {
        const len = queue.length;
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            result++;
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        };
    };
    return result;
}

// 利用完全二叉树性质递归遍历
var countNodes = root => {
    if (!root) return 0;
    let left = root.left;
    let right = root.right;
    let leftDepth = 0;
    let rightDepth = 0;
    while(left) {
        left = left.left;
        leftDepth++;
    }
    while(right) {
        right = right.right;
        rightDepth++;
    };
    if (leftDepth === rightDepth) {
        return Math.pow(2, leftDepth + 1) - 1;
    };
    return countNodes(root.left) + countNodes(root.right) + 1;
}
```

### 求所有路径
```javascript
var binaryTreePaths = function(root) {
    const res = [];
    const getRoad = (node, curPath) => {
        if (!node.left && !node.right) {
            curPath += node.val;
            res.push(curPath);
            return;
        }
        curPath += node.val + '->';
        node.left && getRoad(node.left, curPath);
        node.right && getRoad(node.right, curPath);
    };
    getRoad(root, '');
    return res;
};
```
```javascript
var binaryTreePaths = function(root) {
    if (!root) return [];
    const stack = [root];
    const res = [];
    const path = [''];
    while(stack.length) {
        const node = stack.pop();
        let curPath = path.pop();
        if (!node.left && !node.right) {
            curPath += node.val;
            res.push(curPath);
            continue;
        };
        curPath += node.val + '->';
        node.right && stack.push(node.right) && path.push(curPath);
        node.left && stack.push(node.left) && path.push(curPath);
    }
    return res;
};
```

### 求左叶子之和
```javascript
var sumOfLeftLeaves = function(root) {
  const getLeftVal = node => {
      if (!node) return 0;

      let sum = 0;
      let left = getLeftVal(node.left);
      let right = getLeftVal(node.right);

      let midVal = 0;
      // 这里midVal就是叶子节点，为什么是这样算呢？它把计算时刻提到 “遍历到中间节点”时刻
      if (node.left && !node.left.left && !node.left.right) {
          midVal = node.left.val;
      };
      sum = left + midVal + right;
      return sum;
  }
  return getLeftVal(root);
};
```
```javascript
var sumOfLeftLeaves = function(root) {
    if (!root) return null;
  
    let res = 0;
    const stack = [];
    stack.push(root);
  
    while (stack.length) {
        const node = stack.pop();
        if (node.left && !node.left.left && !node.left.right) {
            res += node.left.val;
        };
        node.left && stack.push(node.left);
        node.right && stack.push(node.right);
    };
    return res;
};
```

### 找树左下角值
```javascript
var findBottomLeftValue = function(root) {
    if (!root) return;
    const res = [];
    const queue = [];
    queue.push(root);
    while(queue.length) {
        const len = queue.length;
        const cur = [];
        for (let i = 0; i < len; i++) {
            const node = queue.shift();
            cur.push(node.val);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        };
        res.push(cur);
    };
    return res[res.length - 1][0];
};
```

### 路径总和
```javascript
var hasPathSum = function(root, targetSum) {
    const traverse = (node, cnt) => {
        if (cnt === 0 && !node.left && !node.right) return true;
        if (!node.left && !node.right) return false;
        if (node.left && traverse(node.left, cnt - node.left.val)) return true;
        if (node.right && traverse(node.right, cnt - node.right.val)) return true;
        return false;
    };
    if (!root) return false;
    return traverse(root, targetSum - root.val);
};
```
```javascript
var hasPathSum = function (root, targetSum) {
    if (!root) return false;

    const queue = [];
    const res = [];
    queue.push(root);
    res.push(targetSum);

    while (queue.length) {
        const node = queue.shift();
        const val = res.shift();
        let reduceVal = val - node.val;

        if (reduceVal === 0 && !node.left && !node.right) return true;
        node.left && queue.push(node.left) && res.push(reduceVal);
        node.right && queue.push(node.right) && res.push(reduceVal);
    };
    return false;
}
```


### 根据前序遍历&中序遍历构造二叉树
```javascript
var buildTree = function(preorder, inorder) {
    if (!preorder.length) return null;
    const rootVal = preorder.shift();
    const rootIndex = inorder.indexOf(rootVal);
    let root = new TreeNode(rootVal);
    root.left = buildTree(preorder.slice(0, rootIndex), inorder.slice(0, rootIndex));
    root.right = buildTree(preorder.slice(rootIndex), inorder.slice(rootIndex + 1));
    return root;
};
```

### 根据中序遍历&后序遍历构造二叉树
```javascript
var buildTree = function(inorder, postorder) {
    if (!inorder.length) return null;
    const rootVal = postorder.pop(); // 后续遍历最后一个为根节点
    const rootIndex = inorder.indexOf(rootVal);
    let root = new TreeNode(rootVal); // 构造二叉树的根节点
    root.left = buildTree(inorder.slice(0, rootIndex), postorder.slice(0, rootIndex));
    root.right = buildTree(inorder.slice(rootIndex + 1), postorder.slice(rootIndex)); // 此时postorder已经pop了根节点
    return root;
};
```

### 求最大二叉树
![20210204154534796.png](https://cdn.nlark.com/yuque/0/2023/png/26762664/1681046953075-f725a823-cd51-4363-a773-49e43a920bf7.png#averageHue=%23f2f2f2&clientId=ud184a7a1-e85f-4&from=drop&id=u863c1acd&originHeight=432&originWidth=928&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=26483&status=done&style=none&taskId=ude794513-8682-4e9c-bcb5-1d24aff2ed0&title=)
```javascript
var constructMaximumBinaryTree = function(nums) {
    if (!nums.length) return null;
    let rootVal = Math.max(...nums);
    let rootIndex = nums.indexOf(rootVal);
    let root = new TreeNode(rootVal);
    root.left = constructMaximumBinaryTree(nums.slice(0, rootIndex));
    root.right = constructMaximumBinaryTree(nums.slice(rootIndex + 1));
    return root;
};
```

### 合并二叉树
```javascript
var mergeTrees = function(root1, root2) {
    const mergeTree = (root1, root2) => {
        // root1为null，则返回root2
        if (!root1) return root2;
        if (!root2) return root1;

        root1.val += root2.val;
        root1.left = mergeTree(root1.left, root2.left);
        root1.right = mergeTree(root1.right, root2.right);
        return root1;
    };
    return mergeTree(root1, root2);
};
```
```javascript
var mergeTrees = function(root1, root2) {
    if (!root1) return root2;
    if (!root2) return root1;
    const queue = [];
    queue.push(root1);
    queue.push(root2);
    while (queue.length) {
        const node1 = queue.shift();
        const node2 = queue.shift();
        node1.val += node2.val;
        if (node1.left && node2.left) {
            queue.push(node1.left, node2.left);
        };
        if (node1.right && node2.right) {
            queue.push(node1.right, node2.right);
        };
        if (!node1.left && node2.left) node1.left = node2.left;
        if (!node1.right && node2.right) node1.right = node2.right;
    }
    return root1;
};
```

## 二叉搜索树的操作
二叉搜索树有特性：

- 左节点的值小于中间节点
- 右节点的值大于中间节点

这给遍历带来很大程度的便利。

### 搜索
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26762664/1681051290751-67bef4a7-06ed-45a9-b2bb-ccc1c11e5022.png#averageHue=%23f6f6f6&clientId=ud184a7a1-e85f-4&from=paste&height=567&id=u4369b1dc&originHeight=709&originWidth=995&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=34069&status=done&style=none&taskId=u9d3b9639-d96f-48d5-8fed-5b7118c58ea&title=&width=796)
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */
// 递归法
var searchBST = function(root, val) {
    if (!root || root.val === val) return root;
    if (root.val > val) {
        return searchBST(root.left, val);
    };
    if (root.val < val) {
        return searchBST(root.right, val);
    };
    return null;
};
```
```javascript
var searchBST = (root, val) => {
    if (!root) return null;
    const queue = [root];
    while (queue.length) {
        const node = queue.shift();
        if (!node) continue;

        if (node.val > val) {
            queue.push(node.left);
        }else if (node.val < val) {
            queue.push(node.right);
        }else {
            return node;
        }
    };
    return null;
}
```


### 验证是否二叉搜索树
关键点：判断是否升序
```javascript
var isValidBST = function(root) {
    const res = [];
    const midTraverse = root => {
        if (!root) return;
        root.left && midTraverse(root.left);
        res.push(root.val);
        root.right && midTraverse(root.right);
    };
    midTraverse(root);
    for (let i = 0; i < res.length - 1; i++) {
        if (res[i] >= res[i + 1]) return false;
    };
    return true;
};
```

### [二叉搜索树的最小绝对差](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/)
给你一个二叉搜索树的根节点 root ，返回 树中任意两不同节点值之间的最小差值 。
差值是一个正数，其数值等于两值之差的绝对值。
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function(root) {
    let preNode = null;
    let res = Infinity;

    // 中序遍历
    const inorder = node => {
        if (!node) return;
        inorder(node.left);
        if (preNode) res = Math.min(res, node.val - preNode.val);
        // 记录下一个节点
        preNode = node;
        inorder(node.right);
    }
    inorder(root);
    return res;
};
```
```javascript
var getMinimumDifference = function(root) {
    const res = [];
    const inorder = node => {
        if (node) {
            inorder(node.left);
            res.push(node.val);
            inorder(node.right);
        }
    };
    inorder(root);
    let diff = Infinity;
    for (let i = 0; i < res.length - 1; i++) {
        if (diff > res[i + 1] - res[i]) {
            diff = res[i + 1] - res[i];
        }
    };
    return diff;
};
```

### [501. 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */

// 使用额外空间
var findMode = function(root) {
    let map = new Map();

    // 中序遍历且构造好map
    const inorder = node => {
        if (!node) return;
        inorder(node.left);
        map.set(node.val, map.has(node.val)? map.get(node.val) + 1 : 1);
        inorder(node.right);
    };
    inorder(root);

    // map -> { val: 次数 }
    let res = [];
    let mode = map.get(root.val);
    for (let [key, val] of map) {
        if (val === mode) {
            res.push(key);
        }else if (val > mode) {
            res = [];
            mode = val;
            res.push(key);
        }
    };
    return res;
};
```
```javascript
var findMode = function (root) {
    let count = 0, maxCount = 1;
    let res = [], pre = root;
    const inorder = node => {
        if (!node) return;
        inorder(node.left);
        // 单层递归
        if (node.val === pre.val) {
            count++;
        }else {
            count = 1;
        }
        pre = node; // keyCode

        if (count === maxCount) {
            res.push(node.val);
        }else if (count > maxCount){
            res = []; // keyCode
            res.push(node.val); // keyCode
            maxCount = count; // keyCode
        }
        inorder(node.right);
    };
    inorder(root);
    return res;
}
```


### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */

// 后序遍历回溯
var lowestCommonAncestor = function(root, p, q) {
    const backOrder = (root, p, q) => {
        // 递归停止的条件
        if (root === null || root === p || root === q) {
            return root;
        }
        // 左节点进入递归
        let left = backOrder(root.left, p, q);
        // 右节点进入递归
        let right = backOrder(root.right, p, q);

        // 找到公共祖先
        if (left && right) {
            return root;
        }
        // 左边是null返回右边，否则返回左边
        if (!left) return right;
        return left;
    };
    return backOrder(root, p, q);
};
```

### [235. 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)
```javascript
var lowestCommonAncestor = function(root, p, q) {
    while (root) {
        if (!root) return;
        if (root.val < p.val && root.val < q.val) {
            root = root.right;
        }else if (root.val > q.val && root.val > p.val) {
            root = root.left;
        }else {
            return root;
        }
    };
    return null;
};
```

### [701. 二叉搜索树中的插入操作](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)
> 给定二叉搜索树（BST）的根节点 root 和要插入树中的值 value ，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据 保证 ，新值和原始二叉搜索树中的任意节点值都不同。
> 注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回 任意有效的结果 。

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */

// 无返回值的递归
var insertIntoBST = function(root, val) {
    const setInOrder = (root, val) => {
        if (!root) {
            // 当遇到null节点，则插入位置找到了
            let node = new TreeNode(val);
            return node;
        }
        // 根据二叉搜索树的特性，大于中间节点的插入右边，小于的插入左边
        if (val > root.val) {
            root.right = setInOrder(root.right, val);
        }
        if (val < root.val) {
            root.left = setInOrder(root.left, val);
        }
        // 这里return出去后，root.left | root.right 才能捕获到节点
        return root;
    };
    return setInOrder(root, val);
};
```
```javascript
// 有返回值的递归
var insertIntoBST = function (root, val) {
    if (!root) return new TreeNode(val);
    // if (!root) root = new TreeNode(val);

    let parent = null;
    const preOrder = (cur, val)  => {
        if (!cur) {
            let node = new TreeNode(val);
            if (parent.val > val) {
                parent.left = node;
            }else {
                parent.right = node;
            }
            return;
        }
        parent = cur;
        if (cur.val > val) {
            preOrder(cur.left, val);
        }
        if (cur.val < val) {
            preOrder(cur.right, val);
        }
    }
    preOrder(root, val);
    return root;
}
```
```javascript
// 迭代法 -- 遍历到插入位置后插入
var insertIntoBST = function (root, val) {
    if (!root) {
        root = new TreeNode(val)
    }else {
        let parent = null;
        let cur = root; // 这里再用一个指针指向root而不是直接用root去遍历更新，使得最后返回root不会空
        while(cur) {
            parent = cur;
            if (val > cur.val) {
                cur = cur.right;
            }else if (val < cur.val) {
                cur = cur.left;
            }
        }
        // 此时找到合适的位置了
        let node = new TreeNode(val);
        if (parent.val > val) {
            parent.left = node;
        }else {
            parent.right = node;
        }
    }
    return root;
}
```

### [450. 删除二叉搜索树中的节点](https://leetcode.cn/problems/delete-node-in-a-bst/)
```javascript
var deleteNode = function(root, key) {
    if (!root) return null;
    if (key > root.val) {
        root.right = deleteNode(root.right, key);
        return root;
    }
    if (key < root.val) {
        root.left = deleteNode(root.left, key);
        return root;
    }
    // key === root.val

    // 左右节点为空或者一个为空的场景
    if (!root.left && !root.right) return null;
    if (root.left && !root.right) return root.left;
    if (!root.left && root.right) return root.right;

    // 左右节点都不为空的场景
    let node = root.right;
    while (node.left) {
        node = node.left;
    }
    // 此时node是待删除结点的右子树中最小的节点--下面是转换操作，keyCode

    // 待删除节点值换成最小节点值
    root.val = node.val;
    // 去掉最小节点
    root.right = deleteNode(root.right, node.val);
    // 上述两步中待删除的左节点不用动
    
    return root;
};
```

### [669. 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree/)
```javascript
// 递归法
var trimBST = function (root, low, high) {
    if (!root) return null;
    if (root.val < low) {
        let right = trimBST(root.right, low, high);
        return right;
    }
    if (root.val > high) {
        let left = trimBST(root.left, low, high);
        return left;
    }
    root.left = trimBST(root.left, low, high);
    root.right = trimBST(root.right, low, high);
    return root;
}
```
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} low
 * @param {number} high
 * @return {TreeNode}
 */
var trimBST = function(root, low, high) {
    if (!root) return null;
    // 删除节点，什么时候删除？如何删除？
    // 到达能删除的地方
    while (root && (root.val < low || root.val > high)) {
        if (root.val < low) {
            root = root.right;
        }else {
            root = root.left;
        }
    }
    let cur = root; // 保存一下root，让cur去前面探查删除节点

    // 删除操作-- 从左子树开始，探查小于low的
    while (cur) {
        while(cur.left && cur.left.val < low) {
            cur.left = cur.left.right; // 将左节点替换为左节点的右子树，因为它左边部分比中间小，中间不考虑自然左子树不用考虑
        }
        cur = cur.left;
    }

    cur = root // 还原

    // 从右子树开始，探查大于high的
    while (cur) {
        while(cur.right && cur.right.val > high) {
            cur.right = cur.right.left; // 同上
        }
        cur = cur.right;
    }
    return root;
};
```


### [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)
```javascript
// 递归法
var sortedArrayToBST = (nums) => {
    const buildTree = (arr, left, right) => {
        if (left > right) return null;
        let mid = Math.floor(left + (right - left) / 2); // 注意js里处理数字常用到Math对象里面的方法
        let root = new TreeNode(arr[mid]);
        root.left = buildTree(arr, left, mid - 1);
        root.right = buildTree(arr, mid + 1, right);
        return root;
    };
    return buildTree(nums, 0, nums.length - 1);
}
```

### [538. 把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/)
```javascript
var convertBST = function(root) {
    let pre = null;
    const sumTree = (node) => {
        if (!node) return;
        node.right && sumTree(node.right);
        
        if (pre) {
            node.val += pre.val;
        }

        pre = node;
        node.left && sumTree(node.left);
    };
    sumTree(root);
    return root;
};
```

# 回溯思想

### [77. 组合](https://leetcode.cn/problems/combinations/)
给定两个整数 n 和 k，返回范围 [1, n] 中所有可能的 k 个数的组合。
你可以按 **任何顺序** 返回答案。
```javascript
let path = []; // 存放路径
let result = []; // 存放结果集
const combine = (n, k) => {
    result = [];
    combineFind(n, k ,1); // 从 1 开始
    return result;
}
const combineFind = (n, k, startIndex) => {
    if (path.length === k) { // 满足要求推进结果集
        result.push([...path]);
        return;
    }
    for (let i = startIndex; i <= n - (k - path.length) + 1; i++) {
        path.push(i); // 深度往下加
        combineFind(n, k, i + 1);
        path.pop(); // 回溯，深度往上减
    }
}
```

### [216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)
```javascript
/**
 * @param {number} k
 * @param {number} n
 * @return {number[][]}
 */
var combinationSum3 = function(k, n) {
    let result = [];
    let path = [];
    let sum = 0;
    const dfs = (path, index) => {
        if (sum > n) return;
        if (path.length === k) {
            if (sum === n) {
                result.push([...path]);
                return;
            }
        }
        for (let i = index; i <= 9 - (k - path.length) + 1; i++) {
            path.push(i);
            sum += i;
            dfs(path, ++index);
            sum -= i;
            path.pop();
        }
    }
    dfs(path, 1);
    return result;
};
```

### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/26762664/1681830759309-4b65b952-a515-42ba-93ee-9327f3c15e19.png#averageHue=%23e2e1e1&clientId=u240e7b63-004f-4&from=paste&height=339&id=u793cf607&originHeight=424&originWidth=795&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=87149&status=done&style=none&taskId=u20c1673f-d61f-4eb4-a1a0-4ce07b7ff04&title=&width=636)
```javascript
var letterCombinations = digits => {
    let k = digits.length; // 记录按了几个按钮
    let mapArr = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"]; // 对应数字->数组索引逻辑一致去匹配,比如号码 2 对应的映射即数组第二个
    if (!k) return [];
    if (k === 1) return mapArr[digits].split(""); // digits即为索引，比如输入"2" => ['a','b','c']
    const res = [];// 存储结果和记录path
    let path = [];
    dfs(digits, k, 0);
    return res;

    function dfs (digits, k, n) {
        if (path.length === k) {
            res.push(path.join(""));
            return;
        }
        for (const str of mapArr[digits[n]]) {
            path.push(str);
            dfs(digits, k, n + 1);
            path.pop(); // 回溯
        }
    }
}
```


### [39. 组合总和](https://leetcode.cn/problems/combination-sum/)
```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */

// 其实相比77题，就是每个数支持重复使用
// 本题的解法: [1, 2, 3], target = 10, 一开始会先走10个1，接着退出一些1来用2弥补等等，这个过程用“if (val > target - sum) break; ”剪枝优化下
const combinationSum = function(candidates, target) {
    candidates.sort((a, b) => a - b); // 会改变原数组
    if (!candidates.length || candidates[0] > target) return [];
    const res = [], path = [];
    findCombination(candidates, 0, 0);
    function findCombination(candidates, index, sum) {
        if (sum === target) {
            res.push([...path]);
            return;
        }
        for (let i = index; i < candidates.length; i++) {
            const val = candidates[i];
            if (val > target - sum) break;
            sum += val;
            path.push(val);
            findCombination(candidates, i, sum); // 此时 i 原封不动传入
            sum -= val; // 回溯
            path.pop(); // 回溯
        }
    }
    return res;
};
```


### [40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)
```javascript
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
```

###  [131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)
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

### [78. 子集](https://leetcode.cn/problems/subsets/submissions/)

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 * 
 * when input [1,2,3]
 * sholud output [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
 */
const subsets = (nums) => {
    const res = [], path = [], len = nums.length;
    getSubset(0);
    return res;
    function getSubset(index) {
        res.push([...path]);

        for (let i = index; i < len; i++) {
            path.push(nums[i]);
            getSubset(i + 1);
            path.pop();
        }
    }
}
```

### [90. 子集 II](https://leetcode.cn/problems/subsets-ii/)
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

### [491. 递增子序列](https://leetcode.cn/problems/non-decreasing-subsequences/)
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */

const findSubsequences = (nums) => {
    const res = [], path = [], len = nums.length;
    getSubsequences(0);
    return res;
    function getSubsequences(index) {
        if (path.length > 1) {
            res.push([...path]);
        }
        let map = new Map(); // 记录同一层是否使用相同数字
        for (let i = index; i < len; i++) {
            if (path.length > 0 && nums[i] < path[path.length - 1] || map.has(nums[i])) {
                continue;
            }
            map.set(nums[i], 1);
            path.push(nums[i]);
            getSubsequences(i + 1);
            path.pop();
        }
    }
}
```

### [46. 全排列](https://leetcode.cn/problems/permutations/)
```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
// 排列和组合区别在于是否有序，[1, 2] 和 [2, 1]为两个集合，这使得取值推进 path 时，核心是判断同一 path 是否已经使用元素
const permute = (nums) => {
    const res = [], path = [], len = nums.length;
    const hasUse = new Array(len).fill(0); // nums[1, 2, 3] -> hasUse[0, 0 ,0]  0: 没使用 1: 使用
    getPermute(hasUse);
    return res;
    function getPermute(hasUse) {
        if (path.length === len) {
            res.push([...path]);
            return; // TODO lc-491没有return，是为了找到树中所有节点，此题找到叶子节点（长度为nums长度）则可以返回，具体细节需要再去理解下
        }
        for (let i = 0; i < len; i++) {
            if (hasUse[i]) continue;
            hasUse[i] = 1;
            path.push(nums[i]);
            getPermute(hasUse);
            hasUse[i] = 0;
            path.pop();
        }
    }
}
```

![代码随想录](https://code-thinking-1253855093.file.myqcloud.com/pics/20211027181706.png)




### [47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)
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




### [332. 重新安排行程](https://leetcode.cn/problems/reconstruct-itinerary/)
```javascript
/**
 * @param {string[][]} tickets
 * @return {string[]}
 */
const findItinerary = function(tickets) {
    let result = ['JFK'];
    let map = {};
    for (const ticket of tickets) {
        let [from, to] = ticket;
        if (!map[from]) {
            map[from] = [];
        }
        map[from].push(to);
    }
    
    for (const city in map) {
        // 对到达城市列表排序
        map[city].sort()
    }
    
    getItinerary();
    return result;

    function getItinerary() {
        if (result.length === tickets.length + 1) return true;
        if (!map[result[result.length - 1]]) return false;
        for (let i = 0; i < map[result[result.length - 1]].length; i++) {
            let nextCity = map[result[result.length - 1]][i];
            map[result[result.length - 1]].splice(i, 1);
            result.push(nextCity);
            if (getItinerary()) return true;
            result.pop();
            map[result[result.length - 1]].splice(i, 0, nextCity);
            
        }
    }
};
```


### [51. N 皇后](https://leetcode.cn/problems/n-queens/)
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



### [37. 解数独](https://leetcode.cn/problems/sudoku-solver/)
```javascript
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
// TODO 值得再深思做下
const solveSudoku = (board) => {
    const isValid = (row, col, val, board) => {
        const len = board.length
        // 行不能重复
        for(let i = 0; i < len; i++) {
            if(board[row][i] === val) {
                return false
            }
        }
        // 列不能重复
        for(let i = 0; i < len; i++) {
            if(board[i][col] === val) {
                return false
            }
        }
        const startRow = Math.floor(row / 3) * 3
        const startCol = Math.floor(col / 3) * 3

        for(let i = startRow; i < startRow + 3; i++) {
            for(let j = startCol; j < startCol + 3; j++) {
                if(board[i][j] === val) {
                    return false
                }
            }
        }

        return true
    }

    const backTracking = () => {
        for(let i = 0; i < board.length; i++) {
            for(let j = 0; j < board[0].length; j++) {
                if(board[i][j] !== '.') continue
                for(let val = 1; val <= 9; val++) {
                    if(isValid(i, j, `${val}`, board)) {
                        board[i][j] = `${val}`
                        if (backTracking()) {
                            return true
                        }

                        board[i][j] = `.`
                    }
                }
                return false
            }
        }
        return true
    }
    backTracking(board)
    return board

};
```



# 贪心思想

### [455. 分发饼干](https://leetcode.cn/problems/assign-cookies/)

```javascript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
const findContentChildren = (g, s) => {
    let gI = g.length - 1, sJ = s.length - 1;
    // 排序使得比较有意义
    g.sort( (a, b) => a - b);
    s.sort( (a, b) => a - b);
    let res = 0;
    while (gI >= 0 && sJ >= 0) {
        if (g[gI] <= s[sJ]) {
            res++;
            gI--;
            sJ--;
            continue;
        }
        gI--;
    }
    return res;
}
```

```TypeScript
const findContentChildren = (g: number[], s: number[]) : number => {
    let gI: number = g.length - 1, sJ: number = s.length - 1;
    // 排序使得比较有意义
    g.sort( (a, b) => a - b);
    s.sort( (a, b) => a - b);
    let res: number = 0;
    while (gI >= 0 && sJ >= 0) {
        if (g[gI] <= s[sJ]) {
            res++;
            gI--;
            sJ--;
            continue;
        }
        gI--;
    }
    return res;
}
```

### [376. 摆动序列](https://leetcode.cn/problems/assign-cookies/)
```typescript
function wiggleMaxLength(nums: number[]): number {
    let res: number = 1;
    let preDiff: number = 0, curDiff: number = 0;
    for (let i = 0; i < nums.length; i++){
        curDiff = nums[i + 1] - nums[i];
        // 交替部分-- keyCode
        if ((curDiff > 0 && preDiff <= 0) || (curDiff < 0 && preDiff >= 0)) {
            res++;
            preDiff = curDiff;
        }
    }
    return res;
}
```

### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)
```typescript
function maxSubArray(nums: number[]): number {
    let res: number = -Infinity;
    let count: number = 0;
    for (let i = 0; i < nums.length; i++) {
        count += nums[i];
        if (count > res) {
            res = count;
        }
        // 重置
        if (count < 0) {
            count = 0;
        }
    }
    return res;
};
```

### [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
```typescript
function maxProfit(prices: number[]): number {
    let result: number = 0;
    for (let i = 1; i < prices.length; i++) {
        // 跨一大步也能拆分成多个小步，小步趋近 5-1 -> 5-4+4-3+3-2+2-1
        result += Math.max((prices[i] - prices[i - 1]), 0);
    }
    return result;
};
```


### [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)
```typescript
function canJump(nums: number[]): boolean {
    const resIndex: number = nums.length - 1;
    let maxCover: number = 0; // 覆盖范围
    if (nums.length === 1) return true;

    for (let i = 0; i < nums.length; i++) {
        maxCover = Math.max(maxCover - 1, nums[i], 0);
        if (maxCover === 0) break;
        if (maxCover + i >= resIndex) return true;
    }
    return false;
}
```


### [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)
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

### [1005. K 次取反后最大化的数组和](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)
```typescript
function largestSumAfterKNegations(nums: number[], k: number): number {
    nums.sort((a, b) => Math.abs(b) - Math.abs(a));
    console.log(nums);
    let curIndex: number = 0;
    const length = nums.length;
    while (curIndex < length && k > 0) {
        if (nums[curIndex] < 0) {
            nums[curIndex] *= -1;
            k--;
        }
        curIndex++;
    }
    while (k > 0) {
        nums[length - 1] *= -1;
        k--;
    }
    return nums.reduce((pre, cur) => pre + cur, 0);
};
```

### [134. 加油站](https://leetcode.cn/problems/gas-station/)
```typescript
// 暴力解法
function canCompleteCircuit(gas: number[], cost: number[]): number {
    const len = gas.length as number;
    // 加油站遍历，如遇到合适的即刻返回起点站
    for (let i = 0; i < len; i++) {
        let hasGas:number = gas[i] - cost[i];
        let recodeRoad:number = (i + 1) % len;
        while (hasGas > 0 && recodeRoad !== i) {
            hasGas += gas[recodeRoad] - cost[recodeRoad];
            recodeRoad = (recodeRoad + 1) % len;
        }
        // 到这里就是hasGas <= 0 || recodeRoad === i
        if (hasGas >= 0 && recodeRoad === i) return i
    }
    return -1
};


// 贪心思想-方法1
// function canCompleteCircuit(gas: number[], cost: number[]): number {
//     let min = Infinity;
//     let hasGas = 0;
//     const len = gas.length;

//     for (let i = 0; i < len; i++) {
//         hasGas += gas[i] - cost[i];
//         if (hasGas < min) {
//             min = hasGas;
//         }

//     }
//     // 1.全部的 gas 小于所需，那么跑步了一圈
//     if (hasGas < 0) return -1;

//     // 2.如果最小的站消耗(gas[i] - cost[i])，那势必走一圈还留存汽油
//     if (min >= 0) return 0;

//     // 3.当 min < 0 时，此时可以从后边站向前遍历，谁能补差就从谁出发
//     for (let i = len - 1; i >= 0; i--) {
//         min += gas[i] - cost[i];
//         if (min >= 0) {
//             return i;
//         }
//     }
//     return -1;
// };

// 贪心思想-方法2
// function canCompleteCircuit(gas: number[], cost: number[]): number {
//     let everyStationGetGas: number = 0;
//     let totalGas: number = 0;
//     let startIndex: number = 0

//     for (let i = 0; i < gas.length; i++) {
//         everyStationGetGas += gas[i] - cost[i];
//         totalGas += gas[i] - cost[i];
//         // 当发现当前站汽油已经不足以支撑去下一站，更新startIndex
//         if (everyStationGetGas < 0) {
//             everyStationGetGas = 0;
//             startIndex = i + 1;
//         }
//     }
//     if (totalGas < 0) return -1;
//     return startIndex;
// };
```

### [135. 分发糖果](https://leetcode.cn/problems/candy/)
```typescript
function candy(ratings: number[]): number {
    if (ratings.length <= 0) return 0;
    const len = ratings.length;
    // 确保每个孩子至少分配1个糖果
    let res = new Array(len).fill(1);

    // 相邻两个孩子评分更高的孩子会获得更多的糖果-右孩子比左孩子高分
    for (let i = 0; i < len - 1; i++) {
        if (ratings[i + 1] > ratings[i]) {
            // 一开始只是res[i + 1]++, 这少思考了如果出现ratings[1,2,3] -> [1,2,2], 应为[1, 2, 3]
            res[i + 1] = res[i] + 1;
        }
    }

    // 相邻两个孩子评分更高的孩子会获得更多的糖果-处于中间的孩子比它的左孩子高分
    for (let i = len - 2; i >= 0; i--) {
        if (ratings[i] > ratings[i + 1]) {
            res[i] = Math.max(res[i], res[i + 1] + 1);
        }
    }
    return res.reduce((cur, pre) => cur + pre);
};

// function candy(ratings: number[]): number {
//     const candies: number[] = [];
//     candies[0] = 1;
//    const len = ratings.length as number;

//     for (let i = 1, length = len; i < length; i++) {
//         if (ratings[i] > ratings[i - 1]) {
//             candies[i] = candies[i - 1] + 1;
//         } else {
//             candies[i] = 1;
//         }
//     }
    
//     for (let i = len - 2; i >= 0; i--) {
//         if (ratings[i] > ratings[i + 1]) {
//             candies[i] = Math.max(candies[i], candies[i + 1] + 1);
//         }
//     }
//     return candies.reduce((pre, cur) => pre + cur);
// };
```


### [860. 柠檬水找零](https://leetcode.cn/problems/lemonade-change/)
```typescript
function lemonadeChange(bills: number[]): boolean {
    let hasMoney: money = {
        five: 0,
        ten: 0,
        twenty: 0
    };
    for (let i: number = 0; i < bills.length; i++) {
        switch(bills[i]) {
            case 5:
                hasMoney.five++;
                break;
            case 10:
                hasMoney.ten++;
                if (hasMoney.five < 1) return false;
                hasMoney.five--;
                break;
            case 20:
                hasMoney.twenty++;  // 5:0 10:0, 20:1、
                if (hasMoney.ten >= 1 && hasMoney.five >= 1) {
                    hasMoney.five--;
                    hasMoney.ten--;
                }else if (hasMoney.five >= 3) {
                    hasMoney.five = hasMoney.five - 3;
                }else {
                    return false;
                }
        }
    }
    return true;
};
interface money {
    five: number,
    ten: number,
    twenty: number
}
```

### [406. 根据身高重建队列](https://leetcode.cn/problems/queue-reconstruction-by-height/)
```typescript
function reconstructQueue(people: number[][]): number[][] {
    const sortedByHeightPeople = people.sort((a, b) => {
        if (a[0] === b[0]) return a[1] - b[1]; // 如果同高，第二个数大的自然在后边
        return b[0] - a[0];
    });
    console.log(sortedByHeightPeople);
    const newPeople: number[][] = [];
    while(sortedByHeightPeople.length) {
        const p = sortedByHeightPeople.shift();
        newPeople.splice(p[1], 0, p);
    }
    return newPeople;
};
```


### [452. 用最少数量的箭引爆气球](https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/)
```typescript
function findMinArrowShots(points: number[][]): number {
    if (!points.length) return 0;

    // 按气球的右边界进行升序
    const sortedPoints = points.sort((a:number[], b:number[]) => a[1] - b[1]);
    let arrow:number = 1;
    let pos:number = sortedPoints[0][1]; // x轴上右边界最靠左的气球
    
    for (let i = 1; i < sortedPoints.length; i++) {
        if (sortedPoints[i][0] > pos) {
            arrow++;
            pos = sortedPoints[i][1];
        }else {
            pos = Math.min(pos, sortedPoints[i][1]);
        }
    }
    return arrow;
};
```


### [435. 无重叠区间](https://leetcode.cn/problems/non-overlapping-intervals/)
```typescript
function eraseOverlapIntervals(intervals: number[][]): number {
    if (!intervals.length) return 0;
    // 以区间尾进行排序
    const sortedIntervals = intervals.sort((a:number[], b:number[]) =>  a[1] -  b[1]);
    console.log(sortedIntervals)
    // 先定义一个临界，然后慢慢逼近终点，这个过程中计算出非交叉区间
    let limit:number = sortedIntervals[0][1];
    // 非交叉区间,初始是1。如果逻辑是直接算交叉区间，则应该初始为0
    let num: number = 1;
    for (let i = 1; i < sortedIntervals.length; i++) {
        //
        if (limit <= sortedIntervals[i][0]) {
            num++;
            limit = sortedIntervals[i][1];
        }
    }
    return intervals.length - num;

    // 非交叉区间,初始是1。如果逻辑是直接算交叉区间，则应该初始为0
    // let num: number = 0;
    // for (let i = 1; i < sortedIntervals.length; i++) {
    //     //
    //     if (limit > sortedIntervals[i][0]) {
    //         num++;
    //         limit = Math.min(limit, sortedIntervals[i][1]);
    //     }else {
    //         limit = sortedIntervals[i][1];
    //     }
    // }
    // return num;
};
```


### [763. 划分字母区间](https://leetcode.cn/problems/partition-labels/)
```typescript
// 被字符串划分为尽可能多的片段混淆，关键点是同一字母最多出现在一个片段中。
function partitionLabels(s: string): number[] {

    // TODO 方向觉得没错，但测试示例没跑满
    // // 用数组索引类比 'a-z'
    // const arr = new Array(26);
    // 计算每个字母最远下标
    // for (let i = 0; i < s.length; i++) {
    //     // @ts-ignore
    //     arr[s.charCodeAt(i) - 'a'.charCodeAt()] = i;
    // }

    const strFarest: Map<string, number> = new Map();
    for (let i = 0; i < s.length; i++) {
        strFarest.set(s[i], i);
    }

    let left = 0;
    let right = strFarest.get(s[0]);
    const result = [];

    
    for (let i = 0; i < s.length; i++) {
        right = Math.max(right, strFarest.get(s[i]));
        if (right === i) {
            result.push(right - left + 1);
            left = right + 1;
        }
    }
    return result;
};

```



### [56. 合并区间](https://leetcode.cn/problems/merge-intervals/)
```typescript
function merge(intervals: number[][]): number[][] {
    const sortedIntervals: number[][] = intervals.sort((a: number[], b: number[]) => a[0] - b[0]);
    const result: number[][] = [];
    console.log(sortedIntervals)
    let limit = sortedIntervals[0];
    result.push(limit);

    for (let i = 1; i < sortedIntervals.length; i++) {
        if (sortedIntervals[i][0] <= limit[1]) {
            result.pop();
            // Math.max是需要的，防止[[1,4],[2,3]] -> [[1,3]]，应为[[1,4]]
            let newLimit = [limit[0], Math.max(limit[1], sortedIntervals[i][1])];
            result.push(newLimit);
            limit = newLimit;
        } else {
            result.push(sortedIntervals[i]);
            // 忘记加下面这一行，导致[[2,3],[2,2],[3,3],[1,3],[5,7],[2,2],[4,6]] —> [[1,3],[4,6],[5,7]]，应为[[1,3],[4,7]]
            limit = sortedIntervals[i];
        }
    }

    return result;
}
```

### [738. 单调递增的数字](https://leetcode.cn/problems/monotone-increasing-digits/)
```typescript
function monotoneIncreasingDigits(n: number): number {
    // 2023.06.04 感觉此题题解破解妙处 保留已排好序+补充9 如 1220 ->  1199
    const numArr: number[] = n.toString().split('').map(i => Number(i));
    const len: number = numArr.length;
    let targetIndex: number = len;

    // 从后向前遍历,获取未排序起始点，即targetIndex
    for (let i = len - 1; i > 0; i--) {
        if (numArr[i - 1] > numArr[i]) {
            targetIndex = i;
            numArr[i - 1]--;
        }
    }

    // 补充9
    for (let i = targetIndex; i < len; i++) {
        numArr[i] = 9;
    }

    return Number(numArr.map(i => i.toString()).join(''));
};
```


### [968. 监控二叉树](https://leetcode.cn/problems/binary-tree-cameras/)
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

function minCameraCover(root: TreeNode | null): number {
    let result = 0;
    // 定义三个状态 0:无覆盖 1:有摄像头 2:有覆盖
    // 1.后序遍历
    const dfs = root => {
        if (!root) return 2; // 空节点属于有覆盖情况
        const left = dfs(root.left);
        const right = dfs(root.right);
        // 2,2 -> 0
        if (left === 2 && right === 2) return 0;
        // 0 | (0 | 2)  -> 1（得放摄像头了）
        if (left === 0 || right === 0) {
            result++;
            return 1;
        }
        // 1 | (0 | 1 | 2) -> 2
        if (left === 1 || right === 1) return 2;
        return -1;
    };

    // 2.根节点可能会被遗漏，即它的两个子节点都是2的情况
    if (dfs(root) === 0) {
        result++;
    };

    return result;
};
```



# 动态规划
### [509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number/)
```typescript
function fib(n: number): number {
    let res: number[] = [];
    res[0] = 0;
    res[1] = 1;
    for (let i = 2; i <= n; i++) {
        res[i] = res[i - 1] + res[i - 2];
    }
    return res[n];
};
```

### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)
```typescript
function climbStairs(n: number): number {
    if (n <= 0) return 0;
    const dp:number[] = [];
    dp[1] = 1;
    dp[2] = 2;
    for (let i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
};
```


### [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)
```typescript
function minCostClimbingStairs(cost: number[]): number {
    // 第一步可从下标 0 | 1 开始
    const dp: number[] = [0, 0];
    // i 要考虑 cost.length 不然计算漏了到达楼顶
    for (let i = 2; i <= cost.length; i++) {
        dp[i] = Math.min((dp[i - 1] + cost[i - 1]), (dp[i - 2] + cost[i - 2]));
    }
    return dp[cost.length];
};
```

### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)
```typescript
function uniquePaths(m: number, n: number): number {
    // 机器人每次走 向下或向左，而初始化时，第一行和第一列均为1，接下来就是加总水平垂直的和
    const dp:number[][] = Array.from(Array(m), () => new Array(n));;
    for (let i = 0; i < m; i++) dp[i][0] = 1;
    for (let i = 0; i < n; i++) dp[0][i] = 1;
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
        }
    }
    return dp[m - 1][n - 1];
};
```

### [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)
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



### [343. 整数拆分](https://leetcode.cn/problems/integer-break/)
```typescript
function integerBreak(n: number): number {
    const dp:number[] = new Array(n + 1).fill(0);
    dp[2] = 1;
    for (let i = 3; i <= n; i++) {
        for (let j = 1; j <= i / 2; j++) {
            dp[i] = Math.max(dp[i], j * dp[i - j], j * (i - j));
        }
    }
    return dp[n];
};
```


### [96. 不同的二叉搜索树](https://leetcode.cn/problems/unique-binary-search-trees/)
```typescript
function numTrees(n: number): number {
    const dp: number[] = [];
    dp[0] = -1;
    dp[1] = 1;
    for (let i = 2; i <= n; i++) {
        dp[i] = 2 * dp[i - 1];
        for (let j = 1, end = i - 1; j < end; j++) {
            dp[i] += dp[j] * dp[end - j];
        }
    }
    return dp[n];
};
```


### [1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/)
```typescript
function lastStoneWeightII(stones: number[]): number {
    const sum: number = stones.reduce((a: number, b:number): number => a + b);
    const target: number = Math.floor(sum / 2);
    const n: number = stones.length;
    const dp: number[] = new Array(target + 1).fill(0);
    for (let i: number = 0; i < n; i++ ) {
        for (let j: number = target; j >= stones[i]; j--) {
            dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
        }
    }
    return sum - dp[target] - dp[target];
};
```

### [494. 目标和](https://leetcode.cn/problems/target-sum/)
```typescript
function findTargetSumWays(nums: number[], target: number): number {
    const sum: number = nums.reduce((a: number, b: number): number => a + b);

    if ((sum + target) % 2 || Math.abs(target) > sum) return 0;
    const left: number = (sum + target) / 2;
    const dp: number[] = new Array(left + 1).fill(0);

    dp[0] = 1;  
    for (let i: number = 0; i < nums.length; i++) {
        for (let j: number = left; j >= nums[i]; j--) {
            dp[j] += dp[j - nums[i]];
        }
    }
    return dp[left];
};
```


### [474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/)
```typescript
type BinaryInfo = { numOfZero: number, numOfOne: number };
function findMaxForm(strs: string[], m: number, n: number): number {
    const goodsNum: number = strs.length;
    const dp: number[][] = new Array(m + 1).fill(0)
        .map(_ => new Array(n + 1).fill(0));
    for (let i = 0; i < goodsNum; i++) {
        const { numOfZero, numOfOne } = countBinary(strs[i]);
        for (let j = m; j >= numOfZero; j--) {
            for (let k = n; k >= numOfOne; k--) {
                dp[j][k] = Math.max(dp[j][k], dp[j - numOfZero][k - numOfOne] + 1);
            }
        }
    }
    return dp[m][n];
};
function countBinary(str: string): BinaryInfo {
    let numOfZero: number = 0,
        numOfOne: number = 0;
    for (let s of str) {
        if (s === '0') {
            numOfZero++;
        } else {
            numOfOne++;
        }
    }
    return { numOfZero, numOfOne };
}
```



### [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/)
```typescript
function change(amount: number, coins: number[]): number {
    // coins[1, 2, 5] amount 5 ->  4 种方式
    const dp:number[] = new Array(amount + 1).fill(0);
    dp[0] = 1;
    const len:number = coins.length;
    // 先遍历物品
    for (let i = 0; i < len; i++) {
        // 其次容量,完全背包是 <= ; 01背包是 >= 关键在于是否可重复拿
        for (let j =  coins[i]; j <= amount; j++) {
            dp[j] += dp[j - coins[i]];
        }
    }
    return dp[amount];
};
```

### [377. 组合总和 Ⅳ](https://leetcode.cn/problems/combination-sum-iv/)
```typescript
function combinationSum4(nums: number[], target: number): number {
    // [1, 2, 3] target 4 -> 7 种组合
    const dp: number[] = new Array(target + 1).fill(0);
    dp[0] = 1;
    for (let i = 0; i <= target; i++) { // 先遍历背包容量
        for (let j = 0; j < nums.length; j++) { // 再遍历物品
            if (i >= nums[j]) {
                dp[i] += dp[i - nums[j]];
            }
        }
    }
    return dp[target];
};
```

### [322. 零钱兑换](https://leetcode.cn/problems/coin-change/)
```typescript
function coinChange(coins: number[], amount: number): number {
    // 先遍历物品还是先遍历容量，考虑点在于 是否在意先后顺序 1，5 和 5，1 对本题来说是否一样？一样则都可以，不一样就要考虑先后
    const dp: number[] = new Array(amount + 1).fill(Infinity);
    dp[0] = 0;
    for (let i = 0; i < coins.length; i++) { // 首先遍历物品
        for (let j = 0; j <= amount; j++) { // 其次遍历容量
            if (j >= coins[i]) {
                dp[j] = Math.min(dp[j - coins[i]] + 1, dp[j]);
            }
            
        }
    }
    // console.log(dp);
    return dp[amount] === Infinity ? -1 : dp[amount];
};
```

### [279. 完全平方数](https://leetcode.cn/problems/perfect-squares/)
```typescript
function numSquares(n: number): number {
    // dp[j] 表示和为 j 的完全平方数的最少数量
    // 物品 容量，初始值只知道 n 为容量，物品在哪？
    const len = Math.ceil(Math.sqrt(n));
    const nums: number[] = new Array(len).fill(0);
    const dp: number[] = new Array(n + 1).fill(Infinity);
    nums[0] = 1;
    dp[0] = 0;
    for (let i = 1; i < len; i++) {
        nums[i] = Math.pow((i + 1), 2);
    }
    // console.log('nums', nums);
    for (let i = 0; i < len; i++) {
        for (let j = 0; j <= n; j++) {
            if (j >= nums[i]) {
                dp[j] = Math.min(dp[j - nums[i]] + 1, dp[j]);
            }
        }
    }
    // console.log('dp', dp);
    return dp[n];
};
```




# 各大排序算法以及时间和空间复杂度
## 冒泡排序[ O(n^2)，O(1) ]
```javascript
function bubbleSort(arr) {
  const len = arr.length;
  const res = JSON.parse(JSON.stringify(arr));
  for (let i = 0; i < len; i++) {
    for (let j = 0; j < len - i - 1; j++) { // 大的都冒泡到后面去了，len- i - 1是减少不必要的循环次数
      if (res[j + 1] < res[j]) {
        [res[j + 1], res[j]] = [res[j], res[j + 1]];
      }
    }
  }
  return res;
}
const arr = [1, 2, -1, 0.5, -100, 200, -1000, 300];
const res = bubbleSort(arr);
console.log('未排完序的', arr);
console.log('排完序的', res);
```

## 插入排序[ O(n^2)，O(1) ]
```javascript
function insertSort(arr) {
  const len = arr.length;
  const res = JSON.parse(JSON.stringify(arr)); 
  for (let i = 0; i < len; i++) { // 定义外层循环次数，用处在于每个数都被拿出来了
    for (let j = i; j > 0; j--) { // 拿出来的这个数要开始从自己位置到开头比对下，需要交换就change
      if (res[j] < res[j - 1]) {
        [res[j], res[j - 1]] = [res[j - 1], res[j]];
      }
    }
  };
  return res;
}
const arr = [1, 2, -1, 0.5, -100, 200, -1000, 300];
const res = insertSort(arr);
console.log('未排完序的', arr);
console.log('排完序的', res);
```
## 快速排序[ O(nlogn)，O(nlogn) ]
```javascript
function quickSort(arr, left, right) {
  left = typeof left !== 'number'? 0 : left;
  right = typeof right !== 'number'? arr.length - 1 : right;
  let selectIndex = undefined;
  if (left < right) {
    selectIndex = getSelectIndex(arr, left, right);
    quickSort(arr, left, selectIndex);
    quickSort(arr, selectIndex + 1, right);
  }
  return arr;
}
function getSelectIndex(arr, left, right) {
  let pivot = left;
  let index = pivot + 1;
  for (let i = index; i <= right; i++) {
    if (arr[i] < arr[pivot]) {
      [arr[i], arr[index]] = [arr[index], arr[i]];
      index++;
    }
  }
  [arr[index - 1], arr[pivot]] = [arr[pivot], arr[index - 1]];
  return index - 1;
}
const arr = [1, 2, -1, 0.5, -100, 200, -1000, 300];
const res = quickSort(JSON.parse(JSON.stringify(arr)));
console.log('未排完序的', arr);
console.log('排完序的', res);
```
## 选择排序[ O(n^2)，O(1) ]
```javascript
function selectSort(arr) {
  const res = JSON.parse(JSON.stringify(arr)); 
  const len = res.length;
  if (!len) return;
  for (let i = 0; i < len; i++) {
    let min = i;
    for (let j = i; j < len; j++) {
      if (res[j] < res[min]) {
        min = j;
      }
    }
    if (min !== i) {
      [res[min], res[i]] = [res[i], res[min]];
    }
  }
  return res;
}
const arr = [1, 2, -1, 0.5, -100, 200, -1000, 300];
const res = selectSort(arr);
console.log('未排完序的', arr);
console.log('排完序的', res);
```
