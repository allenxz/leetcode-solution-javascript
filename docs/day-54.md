##### 962. 最大宽度坡

给定一个整数数组 `A`，*坡*是元组 `(i, j)`，其中  `i < j` 且 `A[i] <= A[j]`。这样的坡的宽度为 `j - i`。

找出 `A` 中的坡的最大宽度，如果不存在，返回 0 。

 

**示例 1：**

```
输入：[6,0,8,2,1,5]
输出：4
解释：
最大宽度的坡为 (i, j) = (1, 5): A[1] = 0 且 A[5] = 5.
```

**示例 2：**

```
输入：[9,8,1,0,1,9,4,0,4,1]
输出：7
解释：
最大宽度的坡为 (i, j) = (2, 9): A[2] = 1 且 A[9] = 1.
```

 

**提示：**

1. `2 <= A.length <= 50000`
2. `0 <= A[i] <= 50000`



##### 解题思路

一开始我想用暴力直接解的，但是发现就算是将一些情况排除后，暴力还是过不了倒数两个测试用例。

这道题得开一个额外的数组B，将数组的索引按它们指向的值从小到大排一下序，如果指向的值相同的就按索引从小到大排

举个例子：

A：[9,8,1,0,1,9,4,0,4,1]

B：[3,7,2,4,9,6,8,1,0,5]

因为A[3]<A[7]<A[2]=A[4]....

排好序以后，我们遍历B，记录目前遇到的值最小的索引为`minIndex`，`B[i]-minIndex`即为一个候选宽度，边遍历边对比就能得到最大宽度



##### 代码

```javascript
/**
 * @param {number[]} A
 * @return {number}
 */
var maxWidthRamp = function(A) {
    let len=A.length;
    let B=new Array(len);
    let maxWidth=0;
    for(let i=0;i<len;i++){
        B[i]=i;
    }
    B.sort((a,b)=>{
        if(A[a]===A[b])
            return a-b;
        else
            return A[a]-A[b];
    });
    let minIndex=len;
    for(let i=0;i<len;i++){
        maxWidth=Math.max(maxWidth,B[i]-minIndex);
        minIndex=Math.min(minIndex,B[i]);
    }
    return maxWidth;
};
```

